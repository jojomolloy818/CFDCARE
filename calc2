import React, { useMemo, useState } from "react";

const FOOD_GROUPS = ["Starch", "Protein", "Veg", "Fruit", "Dairy", "Fat"];
const MEALS = ["Breakfast", "AM Snack", "Lunch", "PM Snack", "Dinner", "HS Snack"];
const KCAL_AVG = {
  Starch: 100,
  Protein: 65,
  Veg: 25,
  Fruit: 60,
  Dairy: 110,
  Fat: 75,
  Unassigned: 70,
};

const MEAL_PLAN_BREAKDOWNS = [
  { Starch: 5, Protein: 5, Veg: 2, Fruit: 2, Dairy: 1, Fat: 4 },
  { Starch: 6, Protein: 5, Veg: 2, Fruit: 2, Dairy: 2, Fat: 4 },
  { Starch: 6, Protein: 5, Veg: 2, Fruit: 3, Dairy: 2, Fat: 5 },
  { Starch: 7, Protein: 6, Veg: 2, Fruit: 3, Dairy: 2, Fat: 6 },
  { Starch: 9, Protein: 7, Veg: 2, Fruit: 3, Dairy: 3, Fat: 6 },
  { Starch: 10, Protein: 8, Veg: 2, Fruit: 3, Dairy: 3, Fat: 7 },
  { Starch: 12, Protein: 8, Veg: 2, Fruit: 3, Dairy: 3, Fat: 8 },
  { Starch: 13, Protein: 9, Veg: 2, Fruit: 3, Dairy: 3, Fat: 8 },
  { Starch: 14, Protein: 10, Veg: 2, Fruit: 3, Dairy: 3, Fat: 10 },
  { Starch: 15, Protein: 10, Veg: 2, Fruit: 4, Dairy: 3, Fat: 10 },
  { Starch: 16, Protein: 10, Veg: 3, Fruit: 4, Dairy: 4, Fat: 10 },
  { Starch: 18, Protein: 10, Veg: 3, Fruit: 4, Dairy: 4, Fat: 11 },
  { Starch: 18, Protein: 12, Veg: 3, Fruit: 4, Dairy: 4, Fat: 11 },
  { Starch: 22, Protein: 13, Veg: 5, Fruit: 5, Dairy: 4, Fat: 11 },
  { Starch: 26, Protein: 13, Veg: 5, Fruit: 6, Dairy: 4, Fat: 14 },
].map((row) => ({
  ...row,
  totalKcal: FOOD_GROUPS.reduce((sum, group) => sum + row[group] * KCAL_AVG[group], 0),
}));

const CARE_PLAN_LOOKUP = [
  {
    Breakfast: { Starch: 1, Protein: 1, Veg: 0, Fruit: 1, Dairy: 0, Fat: 1 },
    "AM Snack": { Starch: 0, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 1, Protein: 1, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 0 },
    Dinner: { Starch: 1, Protein: 1, Veg: 1, Fruit: 0, Dairy: 0, Fat: 1 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
  },
  {
    Breakfast: { Starch: 1, Protein: 1, Veg: 0, Fruit: 1, Dairy: 0, Fat: 1 },
    "AM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 1, Protein: 2, Veg: 1, Fruit: 0, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 1, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
  },
  {
    Breakfast: { Starch: 1, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 1 },
    "AM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 1, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Dinner: { Starch: 1, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
  },
  {
    Breakfast: { Starch: 2, Protein: 1, Veg: 0, Fruit: 1, Dairy: 0, Fat: 1 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 1, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
    Dinner: { Starch: 1, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 2, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 1 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 2, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
    Dinner: { Starch: 2, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 3, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 1 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 2, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 1 },
    "PM Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
    Dinner: { Starch: 2, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 3, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 3, Protein: 2, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 3, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 4, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 3, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 3, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 4, Protein: 2, Veg: 0, Fruit: 1, Dairy: 1, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 4, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 3 },
    "PM Snack": { Starch: 0, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
    Dinner: { Starch: 4, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 2 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 4, Protein: 2, Veg: 0, Fruit: 1, Dairy: 1, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 4, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 3 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 4, Protein: 3, Veg: 1, Fruit: 2, Dairy: 0, Fat: 3 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 4, Protein: 2, Veg: 0, Fruit: 1, Dairy: 2, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 4, Protein: 3, Veg: 2, Fruit: 2, Dairy: 0, Fat: 2 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 5, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 4 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 4, Protein: 2, Veg: 0, Fruit: 2, Dairy: 2, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 5, Protein: 3, Veg: 2, Fruit: 1, Dairy: 0, Fat: 3 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 6, Protein: 3, Veg: 1, Fruit: 1, Dairy: 0, Fat: 4 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 5, Protein: 2, Veg: 0, Fruit: 2, Dairy: 2, Fat: 2 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 1 },
    Lunch: { Starch: 5, Protein: 4, Veg: 2, Fruit: 1, Dairy: 0, Fat: 3 },
    "PM Snack": { Starch: 0, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
    Dinner: { Starch: 6, Protein: 4, Veg: 1, Fruit: 1, Dairy: 0, Fat: 3 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 6, Protein: 3, Veg: 0, Fruit: 2, Dairy: 2, Fat: 2 },
    "AM Snack": { Starch: 2, Protein: 1, Veg: 0, Fruit: 0, Dairy: 0, Fat: 0 },
    Lunch: { Starch: 6, Protein: 4, Veg: 2, Fruit: 1, Dairy: 0, Fat: 5 },
    "PM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 0, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 6, Protein: 4, Veg: 3, Fruit: 2, Dairy: 0, Fat: 3 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
  {
    Breakfast: { Starch: 8, Protein: 3, Veg: 0, Fruit: 2, Dairy: 2, Fat: 3 },
    "AM Snack": { Starch: 1, Protein: 1, Veg: 0, Fruit: 1, Dairy: 0, Fat: 0 },
    Lunch: { Starch: 7, Protein: 4, Veg: 2, Fruit: 1, Dairy: 0, Fat: 7 },
    "PM Snack": { Starch: 0, Protein: 1, Veg: 0, Fruit: 1, Dairy: 1, Fat: 0 },
    Dinner: { Starch: 9, Protein: 4, Veg: 3, Fruit: 1, Dairy: 0, Fat: 3 },
    "HS Snack": { Starch: 1, Protein: 0, Veg: 0, Fruit: 0, Dairy: 1, Fat: 1 },
  },
];

const SUPPLEMENT_KCAL_PER_UNIT = {
  "Boost/Ensure Plus": 45,
  "Kate Farms": 45,
  "Clif Bar": 250,
  "Med Plus 2.0": 55,
};

function toNumber(value) {
  const n = Number(value);
  return Number.isFinite(n) ? n : 0;
}

function format(value, digits = 0) {
  return new Intl.NumberFormat("en-US", {
    minimumFractionDigits: digits,
    maximumFractionDigits: digits,
  }).format(value);
}

function buildFoodGroupTotals(carePlan) {
  return FOOD_GROUPS.reduce((acc, group) => {
    acc[group] = MEALS.reduce((sum, meal) => sum + carePlan[meal][group], 0);
    return acc;
  }, {});
}

export default function Page() {
  const [weightLbs, setWeightLbs] = useState(109);
  const [bmrEer, setBmrEer] = useState(1710);
  const [kcalKg, setKcalKg] = useState(45);
  const [supplements, setSupplements] = useState({
    "Boost/Ensure Plus": 0,
    "Kate Farms": 0,
    "Clif Bar": 0,
    "Med Plus 2.0": 0,
  });

  const weightKg = useMemo(() => {
    if (!weightLbs) return 0;
    return Math.round((toNumber(weightLbs) / 2.2) * 10) / 10;
  }, [weightLbs]);

  const wtBasedKcal = useMemo(() => {
    if (!weightKg || !kcalKg) return 0;
    return Math.round(weightKg * toNumber(kcalKg));
  }, [weightKg, kcalKg]);

  const targetKcal = Math.max(toNumber(bmrEer), wtBasedKcal);

  const matched = useMemo(() => {
    return MEAL_PLAN_BREAKDOWNS.map((plan, index) => ({
      ...plan,
      index,
      delta: Math.abs(plan.totalKcal - targetKcal),
      carePlan: CARE_PLAN_LOOKUP[index],
    })).sort((a, b) => a.delta - b.delta)[0];
  }, [targetKcal]);

  const foodGroupTotals = useMemo(() => buildFoodGroupTotals(matched.carePlan), [matched]);

  const mealRows = useMemo(() => {
    return MEALS.map((meal) => {
      const row = matched.carePlan[meal];
      const mealServings = FOOD_GROUPS.reduce((sum, group) => sum + row[group], 0);
      const kcalMeal = FOOD_GROUPS.reduce((sum, group) => sum + row[group] * KCAL_AVG[group], 0);
      return { meal, ...row, mealServings, kcalMeal };
    });
  }, [matched]);

  const mealPlanKcal = FOOD_GROUPS.reduce((sum, group) => sum + matched[group] * KCAL_AVG[group], 0);
  const carePlanKcal = FOOD_GROUPS.reduce((sum, group) => sum + foodGroupTotals[group] * KCAL_AVG[group], 0);
  const varianceToTarget = matched.totalKcal - targetKcal;
  const varianceToPrescription = carePlanKcal - mealPlanKcal;

  const supplementRows = Object.entries(SUPPLEMENT_KCAL_PER_UNIT).map(([name, kcalPerUnit]) => ({
    name,
    units: toNumber(supplements[name]),
    kcal: toNumber(supplements[name]) * kcalPerUnit,
  }));

  const supplementTotal = supplementRows.reduce((sum, row) => sum + row.kcal, 0);
  const totalKcalWithSupplements = carePlanKcal + supplementTotal;

  const dairySplit = (foodGroupTotals.Dairy * KCAL_AVG.Dairy) / 3;
  const macroPct = {
    CHO: carePlanKcal
      ? (((foodGroupTotals.Starch * KCAL_AVG.Starch + foodGroupTotals.Veg * KCAL_AVG.Veg + foodGroupTotals.Fruit * KCAL_AVG.Fruit + dairySplit) / carePlanKcal) * 100)
      : 0,
    PRO: carePlanKcal
      ? (((foodGroupTotals.Protein * KCAL_AVG.Protein + dairySplit) / carePlanKcal) * 100)
      : 0,
    FAT: carePlanKcal
      ? (((foodGroupTotals.Fat * KCAL_AVG.Fat + dairySplit) / carePlanKcal) * 100)
      : 0,
  };

  const snackChecks = ["AM Snack", "PM Snack", "HS Snack"].map((meal) => {
    const row = mealRows.find((item) => item.meal === meal);
    return { meal, servings: row?.mealServings ?? 0, ok: (row?.mealServings ?? 0) <= 3 };
  });

  return (
    <main className="min-h-screen bg-slate-50 text-slate-900">
      <div className="mx-auto max-w-7xl p-6 md:p-8">
        <div className="mb-6">
          <h1 className="text-3xl font-bold tracking-tight">Meal Plan + CARE Plan Calculator</h1>
          <p className="mt-2 text-sm text-slate-600">
            GitHub-friendly Next.js page built from your workbook logic. Paste this into <span className="font-semibold">app/page.tsx</span>.
          </p>
        </div>

        <section className="grid gap-6 lg:grid-cols-3">
          <Panel title="Inputs">
            <Field label="Weight (lbs)" value={weightLbs} onChange={setWeightLbs} />
            <Field label="BMR / EER" value={bmrEer} onChange={setBmrEer} />
            <Field label="kcal / kg" value={kcalKg} onChange={setKcalKg} />
          </Panel>

          <div className="lg:col-span-2 rounded-3xl border border-slate-200 bg-white p-5 shadow-sm">
            <h2 className="mb-4 text-lg font-semibold">Auto Meal Plan Builder</h2>
            <div className="grid gap-4 sm:grid-cols-2 xl:grid-cols-5">
              <MetricCard label="Weight (kg)" value={format(weightKg, 1)} />
              <MetricCard label="Wt-based kcal" value={format(wtBasedKcal)} />
              <MetricCard label="Target kcal" value={format(targetKcal)} />
              <MetricCard label="Matched plan kcal" value={format(matched.totalKcal)} />
              <MetricCard
                label="Variance"
                value={format(varianceToTarget)}
                tone={varianceToTarget === 0 ? "green" : varianceToTarget > 0 ? "amber" : "blue"}
              />
            </div>
          </div>
        </section>

        <section className="mt-6 grid gap-6 xl:grid-cols-[360px,1fr]">
          <div className="rounded-3xl border border-slate-200 bg-white p-5 shadow-sm">
            <h2 className="mb-4 text-lg font-semibold">Recommended Meal Plan Prescription</h2>
            <DataTable
              headers={["Servings", "Food Group", "Kcal"]}
              rows={FOOD_GROUPS.map((group) => [matched[group], group, format(matched[group] * KCAL_AVG[group])])}
              footer={["", "Total Kcal", format(mealPlanKcal)]}
            />
          </div>

          <div className="rounded-3xl border border-slate-200 bg-white p-5 shadow-sm">
            <div className="mb-4 flex flex-wrap items-center justify-between gap-3">
              <h2 className="text-lg font-semibold">CARE Plan Calculator</h2>
              <div className="flex flex-wrap gap-2">
                {snackChecks.map((item) => (
                  <span
                    key={item.meal}
                    className={`rounded-full px-3 py-1 text-xs font-semibold ${
                      item.ok ? "bg-emerald-100 text-emerald-800" : "bg-rose-100 text-rose-800"
                    }`}
                  >
                    {item.meal}: {item.servings} servings {item.ok ? "✓" : "⚠"}
                  </span>
                ))}
              </div>
            </div>

            <div className="overflow-x-auto">
              <table className="min-w-full border-collapse overflow-hidden rounded-2xl border border-slate-200 text-sm">
                <thead className="bg-slate-100">
                  <tr>
                    <th className="px-3 py-2 text-left">Meal</th>
                    {FOOD_GROUPS.map((group) => (
                      <th key={group} className="px-3 py-2 text-center">{group}</th>
                    ))}
                    <th className="px-3 py-2 text-center">Unassigned</th>
                    <th className="px-3 py-2 text-right">Kcal/Meal</th>
                  </tr>
                </thead>
                <tbody>
                  {mealRows.map((row) => (
                    <tr key={row.meal} className="border-t border-slate-200 bg-white">
                      <td className="px-3 py-2 font-medium">{row.meal}</td>
                      {FOOD_GROUPS.map((group) => (
                        <td key={group} className="px-3 py-2 text-center">{row[group]}</td>
                      ))}
                      <td className="px-3 py-2 text-center">0</td>
                      <td className="px-3 py-2 text-right">{format(row.kcalMeal)}</td>
                    </tr>
                  ))}
                  <tr className="border-t border-slate-200 bg-sky-50 font-semibold">
                    <td className="px-3 py-2">Total Guidelines</td>
                    {FOOD_GROUPS.map((group) => (
                      <td key={group} className="px-3 py-2 text-center">{foodGroupTotals[group]}</td>
                    ))}
                    <td className="px-3 py-2 text-center">0</td>
                    <td className="px-3 py-2 text-right">{format(carePlanKcal)}</td>
                  </tr>
                  <tr className="border-t border-slate-200 bg-slate-50 font-semibold">
                    <td className="px-3 py-2">Kcal / Food Group</td>
                    {FOOD_GROUPS.map((group) => (
                      <td key={group} className="px-3 py-2 text-center">{format(foodGroupTotals[group] * KCAL_AVG[group])}</td>
                    ))}
                    <td className="px-3 py-2 text-center">0</td>
                    <td className="px-3 py-2 text-right">{format(carePlanKcal)}</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </section>

        <section className="mt-6 grid gap-6 lg:grid-cols-3">
          <Panel title="Supplements">
            {Object.keys(SUPPLEMENT_KCAL_PER_UNIT).map((name) => (
              <div key={name} className="mb-3 grid grid-cols-[1fr,110px] items-center gap-3 last:mb-0">
                <label className="text-sm font-medium text-slate-700">{name}</label>
                <input
                  type="number"
                  value={supplements[name]}
                  onChange={(e) => setSupplements((prev) => ({ ...prev, [name]: e.target.value }))}
                  className="w-full rounded-xl border border-slate-300 px-3 py-2 text-right outline-none ring-0 transition focus:border-sky-500"
                />
              </div>
            ))}
          </Panel>

          <Panel title="Kcal Validation">
            <InfoRow label="Prescribed kcal" value={mealPlanKcal} />
            <InfoRow label="Distributed kcal" value={carePlanKcal} />
            <InfoRow label="Supplement kcal" value={supplementTotal} />
            <InfoRow label="Total kcal" value={totalKcalWithSupplements} strong />
            <InfoRow label="Variance" value={varianceToPrescription} tone={varianceToPrescription === 0 ? "green" : "amber"} />
          </Panel>

          <Panel title="Estimated Macro Percentages">
            <InfoRow label="CHO" value={macroPct.CHO} suffix="%" digits={1} />
            <InfoRow label="PRO" value={macroPct.PRO} suffix="%" digits={1} />
            <InfoRow label="FAT" value={macroPct.FAT} suffix="%" digits={1} />
          </Panel>
        </section>
      </div>
    </main>
  );
}

function Panel({ title, children }) {
  return (
    <div className="rounded-3xl border border-slate-200 bg-white p-5 shadow-sm">
      <h2 className="mb-4 text-lg font-semibold">{title}</h2>
      {children}
    </div>
  );
}

function Field({ label, value, onChange }) {
  return (
    <label className="mb-4 block last:mb-0">
      <span className="mb-2 block text-sm font-medium text-slate-700">{label}</span>
      <input
        type="number"
        value={value}
        onChange={(e) => onChange(e.target.value)}
        className="w-full rounded-xl border border-slate-300 px-3 py-2 outline-none ring-0 transition focus:border-sky-500"
      />
    </label>
  );
}

function MetricCard({ label, value, tone = "default" }) {
  const toneClass = {
    default: "bg-white",
    green: "bg-emerald-50",
    amber: "bg-amber-50",
    blue: "bg-sky-50",
  }[tone];

  return (
    <div className={`rounded-2xl border border-slate-200 p-4 ${toneClass}`}>
      <div className="text-xs uppercase tracking-wide text-slate-500">{label}</div>
      <div className="mt-1 text-2xl font-semibold">{value}</div>
    </div>
  );
}

function DataTable({ headers, rows, footer }) {
  return (
    <div className="overflow-hidden rounded-2xl border border-slate-200">
      <table className="w-full text-sm">
        <thead className="bg-slate-100">
          <tr>
            {headers.map((header) => (
              <th
                key={header}
                className={`px-3 py-2 font-semibold ${header === "Kcal" ? "text-right" : "text-left"}`}
              >
                {header}
              </th>
            ))}
          </tr>
        </thead>
        <tbody>
          {rows.map((row, index) => (
            <tr key={index} className="border-t border-slate-200 bg-white">
              {row.map((cell, cellIndex) => (
                <td
                  key={cellIndex}
                  className={`px-3 py-2 ${cellIndex === row.length - 1 ? "text-right" : "text-left"}`}
                >
                  {cell}
                </td>
              ))}
            </tr>
          ))}
          <tr className="border-t border-slate-200 bg-slate-50 font-semibold">
            {footer.map((cell, index) => (
              <td key={index} className={`px-3 py-2 ${index === footer.length - 1 ? "text-right" : "text-left"}`}>
                {cell}
              </td>
            ))}
          </tr>
        </tbody>
      </table>
    </div>
  );
}

function InfoRow({ label, value, suffix = "", digits = 0, tone = "default", strong = false }) {
  const colorClass = {
    default: "text-slate-900",
    green: "text-emerald-700",
    amber: "text-amber-700",
  }[tone];

  return (
    <div className="mb-3 flex items-center justify-between rounded-2xl border border-slate-200 px-3 py-2 last:mb-0">
      <span className="text-sm text-slate-600">{label}</span>
      <span className={`text-sm ${colorClass} ${strong ? "font-semibold" : "font-medium"}`}>
        {format(value, digits)}{suffix}
      </span>
    </div>
  );
}
