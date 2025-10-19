import { useState } from "react";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "./ui/card";
import { Button } from "./ui/button";

import { Dialog, DialogContent, DialogDescription, DialogHeader, DialogTitle, DialogTrigger } from "./ui/dialog";
import { Input } from "./ui/input";
import { Label } from "./ui/label";
import { Plus, Apple } from "lucide-react";
import { Badge } from "./ui/badge";

interface Meal {
  id: string;
  name: string;
  calories: number;
  time: string;
  type: "breakfast" | "lunch" | "dinner" | "snack";
}

interface CalorieTrackerProps {
  dailyGoal: number;
  caloriesBurned: number;
}

const mealTypeLabels = {
  breakfast: "Frühstück",
  lunch: "Mittagessen",
  dinner: "Abendessen",
  snack: "Snack",
};

const mealTypeColors = {
  breakfast: "bg-amber-100 text-amber-800 dark:bg-amber-900 dark:text-amber-200",
  lunch: "bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-200",
  dinner: "bg-purple-100 text-purple-800 dark:bg-purple-900 dark:text-purple-200",
  snack: "bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-200",
};

export function CalorieTracker({ dailyGoal, caloriesBurned }: CalorieTrackerProps) {
  const [meals, setMeals] = useState<Meal[]>([
    { id: "1", name: "Haferflocken mit Beeren", calories: 350, time: "07:30", type: "breakfast" },
    { id: "2", name: "Vollkornbrot mit Avocado", calories: 280, time: "10:00", type: "snack" },
    { id: "3", name: "Hähnchen-Salat", calories: 420, time: "12:30", type: "lunch" },
    { id: "4", name: "Griechischer Joghurt", calories: 150, time: "15:00", type: "snack" },
  ]);

  const [isDialogOpen, setIsDialogOpen] = useState(false);
  const [newMeal, setNewMeal] = useState({
    name: "",
    calories: "",
    type: "breakfast" as Meal["type"],
  });

  const caloriesConsumed = meals.reduce((sum, meal) => sum + meal.calories, 0);

  const handleAddMeal = () => {
    if (newMeal.name && newMeal.calories) {
      const now = new Date();
      const timeString = `${now.getHours().toString().padStart(2, "0")}:${now.getMinutes().toString().padStart(2, "0")}`;
      
      setMeals([
        ...meals,
        {
          id: Date.now().toString(),
          name: newMeal.name,
          calories: parseInt(newMeal.calories),
          time: timeString,
          type: newMeal.type,
        },
      ]);
      
      setNewMeal({ name: "", calories: "", type: "breakfast" });
      setIsDialogOpen(false);
    }
  };

  return (
    <Card>
      <CardHeader>
        <div className="flex items-center justify-between">
          <div>
            <CardTitle>Kalorienüberwachung</CardTitle>
            <CardDescription>Tägliche Kalorienbilanz verfolgen</CardDescription>
          </div>
          <Dialog open={isDialogOpen} onOpenChange={setIsDialogOpen}>
            <DialogTrigger asChild>
              <Button size="sm">
                <Plus className="w-4 h-4 mr-2" />
                Mahlzeit
              </Button>
            </DialogTrigger>
            <DialogContent>
              <DialogHeader>
                <DialogTitle>Mahlzeit hinzufügen</DialogTitle>
                <DialogDescription>
                  Erfassen Sie eine neue Mahlzeit oder einen Snack
                </DialogDescription>
              </DialogHeader>
              <div className="grid gap-4 py-4">
                <div className="grid gap-2">
                  <Label htmlFor="meal-name">Name der Mahlzeit</Label>
                  <Input
                    id="meal-name"
                    placeholder="z.B. Spaghetti Bolognese"
                    value={newMeal.name}
                    onChange={(e) => setNewMeal({ ...newMeal, name: e.target.value })}
                  />
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="calories">Kalorien</Label>
                  <Input
                    id="calories"
                    type="number"
                    placeholder="z.B. 450"
                    value={newMeal.calories}
                    onChange={(e) => setNewMeal({ ...newMeal, calories: e.target.value })}
                  />
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="meal-type">Typ</Label>
                  <select
                    id="meal-type"
                    className="flex h-10 w-full rounded-md border border-input bg-input-background px-3 py-2 ring-offset-background focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2"
                    value={newMeal.type}
                    onChange={(e) => setNewMeal({ ...newMeal, type: e.target.value as Meal["type"] })}
                  >
                    <option value="breakfast">Frühstück</option>
                    <option value="lunch">Mittagessen</option>
                    <option value="dinner">Abendessen</option>
                    <option value="snack">Snack</option>
                  </select>
                </div>
              </div>
              <Button onClick={handleAddMeal} className="w-full">
                Mahlzeit hinzufügen
              </Button>
            </DialogContent>
          </Dialog>
        </div>
      </CardHeader>
      <CardContent className="space-y-6">
        <div className="bg-accent rounded-lg p-4">
          <div className="flex items-center gap-2 text-muted-foreground mb-1">
            <Apple className="w-4 h-4" />
            <span className="text-sm">Gegessen</span>
          </div>
          <div className="text-2xl">{caloriesConsumed}</div>
          <div className="text-xs text-muted-foreground">kcal</div>
        </div>

        <div className="space-y-3">
          <h4 className="text-sm text-muted-foreground">Heutige Mahlzeiten</h4>
          <div className="space-y-2">
            {meals.map((meal) => (
              <div key={meal.id} className="flex items-center justify-between p-3 rounded-lg bg-accent">
                <div className="flex-1">
                  <div className="flex items-center gap-2">
                    <span>{meal.name}</span>
                    <Badge variant="secondary" className={mealTypeColors[meal.type]}>
                      {mealTypeLabels[meal.type]}
                    </Badge>
                  </div>
                  <div className="text-sm text-muted-foreground">{meal.time}</div>
                </div>
                <div className="text-right">
                  <div>{meal.calories} kcal</div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </CardContent>
    </Card>
  );
}

