/components
 ├─ GoalCard.tsx
 ├─ DietCard.tsx
 ├─ ExerciseCard.tsx
 └─ Header.tsx
/app/page.tsx
import { Heart } from 'lucide-react'

export function Header() {
  return (
    <div className="bg-white/80 dark:bg-slate-900/80 backdrop-blur-sm border-b sticky top-0 z-10">
      <div className="container mx-auto px-4 py-4">
        <div className="flex items-center gap-3">
          <div className="p-2 bg-gradient-to-r from-green-500 to-emerald-600 rounded-xl">
            <Heart className="w-6 h-6 text-white" />
          </div>
          <div>
            <h1 className="text-2xl font-bold bg-gradient-to-r from-green-600 to-emerald-600 bg-clip-text text-transparent">
              VidaSaudável
            </h1>
            <p className="text-sm text-gray-600 dark:text-gray-400">
              Seu app de emagrecimento saudável
            </p>
          </div>
        </div>
      </div>
    </div>
  )
}
import { Card, CardHeader, CardTitle, CardDescription } from '@/components/ui/card'
import { LucideIcon } from 'lucide-react'

interface GoalCardProps {
  id: string
  title: string
  description: string
  icon: LucideIcon
  color: string
  selected: boolean
  onSelect: (id: string) => void
}

export function GoalCard({ id, title, description, icon: Icon, color, selected, onSelect }: GoalCardProps) {
  return (
    <Card
      className={`cursor-pointer transition-all duration-300 hover:scale-105 hover:shadow-xl ${
        selected ? 'ring-2 ring-green-500 shadow-lg' : 'hover:shadow-lg'
      }`}
      onClick={() => onSelect(id)}
    >
      <CardHeader className="text-center">
        <div className={`w-16 h-16 mx-auto rounded-full bg-gradient-to-r ${color} flex items-center justify-center mb-4`}>
          <Icon className="w-8 h-8 text-white" />
        </div>
        <CardTitle className="text-xl">{title}</CardTitle>
        <CardDescription>{description}</CardDescription>
      </CardHeader>
    </Card>
  )
}
import { Card, CardHeader, CardContent, CardTitle, CardDescription } from '@/components/ui/card'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { ChefHat, Clock, Flame, Play } from 'lucide-react'

interface Recipe {
  name: string
  time: string
  calories: string
  difficulty: string
}

interface DietCardProps {
  id: string
  name: string
  description: string
  benefits: string[]
  recipes: Recipe[]
  onSelect: (id: string) => void
}

export function DietCard({ id, name, description, benefits, recipes, onSelect }: DietCardProps) {
  return (
    <Card className="hover:shadow-lg transition-all duration-300">
      <CardHeader>
        <div className="flex items-center justify-between">
          <CardTitle className="text-lg">{name}</CardTitle>
          <ChefHat className="w-5 h-5 text-green-600" />
        </div>
        <CardDescription>{description}</CardDescription>
      </CardHeader>
      <CardContent className="space-y-4">
        <div className="flex flex-wrap gap-2">
          {benefits.map((benefit, index) => (
            <Badge key={index} variant="secondary" className="text-xs">
              {benefit}
            </Badge>
          ))}
        </div>

        <div className="space-y-3">
          <h4 className="font-semibold text-sm text-gray-900 dark:text-gray-100">
            Receitas Populares:
          </h4>
          {recipes.map((recipe, index) => (
            <div key={index} className="p-3 bg-gray-50 dark:bg-slate-800 rounded-lg">
              <div className="flex items-center justify-between mb-2">
                <h5 className="font-medium text-sm">{recipe.name}</h5>
                <Play className="w-4 h-4 text-green-600" />
              </div>
              <div className="flex items-center gap-4 text-xs text-gray-600 dark:text-gray-400">
                <span className="flex items-center gap-1">
                  <Clock className="w-3 h-3" />
                  {recipe.time}
                </span>
                <span className="flex items-center gap-1">
                  <Flame className="w-3 h-3" />
                  {recipe.calories}
                </span>
                <Badge variant="outline" className="text-xs">
                  {recipe.difficulty}
                </Badge>
              </div>
            </div>
          ))}
        </div>

        <Button
          className="w-full bg-gradient-to-r from-green-500 to-emerald-600 hover:from-green-600 hover:to-emerald-700"
          onClick={() => onSelect(id)}
        >
          Escolher Esta Dieta
        </Button>
      </CardContent>
    </Card>
  )
}
import { Card, CardHeader, CardContent, CardTitle } from '@/components/ui/card'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Clock, Target, Flame, Dumbbell, Play } from 'lucide-react'

interface ExerciseCardProps {
  name: string
  duration: string
  equipment: string
  calories: string
  exercises: string[]
}

export function ExerciseCard({ name, duration, equipment, calories, exercises }: ExerciseCardProps) {
  return (
    <Card className="hover:shadow-lg transition-all duration-300">
      <CardHeader>
        <div className="flex items-center justify-between">
          <CardTitle className="text-lg">{name}</CardTitle>
          <div className="p-2 bg-gradient-to-r from-blue-500 to-indigo-600 rounded-lg">
            <Dumbbell className="w-5 h-5 text-white" />
          </div>
        </div>
      </CardHeader>
      <CardContent className="space-y-4">
        <div className="grid grid-cols-2 gap-4 text-sm">
          <div className="flex items-center gap-2">
            <Clock className="w-4 h-4 text-blue-600" />
            <span>{duration}</span>
          </div>
          <div className="flex items-center gap-2">
            <Target className="w-4 h-4 text-green-600" />
            <span>{equipment}</span>
          </div>
          <div className="flex items-center gap-2 col-span-2">
            <Flame className="w-4 h-4 text-red-600" />
            <span>{calories}</span>
          </div>
        </div>

        <div>
          <h5 className="font-semibold text-sm mb-2">Exercícios inclusos:</h5>
          <div className="flex flex-wrap gap-2">
            {exercises.map((exercise, idx) => (
              <Badge key={idx} variant="outline" className="text-xs">
                {exercise}
              </Badge>
            ))}
          </div>
        </div>

        <Button className="w-full bg-gradient-to-r from-blue-500 to-indigo-600 hover:from-blue-600 hover:to-indigo-700">
          <Play className="w-4 h-4 mr-2" />
          Iniciar Treino
        </Button>
      </CardContent>
    </Card>
  )
}
"use client"

import { useState } from 'react'
import { Header } from '@/components/Header'
import { GoalCard } from '@/components/GoalCard'
import { DietCard } from '@/components/DietCard'
import { ExerciseCard } from '@/components/ExerciseCard'
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
import { Heart, TrendingDown, Activity, Utensils, Dumbbell, Star } from 'lucide-react'
import { Card, CardContent } from '@/components/ui/card'

export default function HealthApp() {
  const [selectedGoal, setSelectedGoal] = useState('')
  const [selectedDiet, setSelectedDiet] = useState('')

  const goals = [
    { id: 'lose-weight', title: 'Perder Peso', description: 'Queimar gordura e emagrecer de forma saudável', icon: TrendingDown, color: 'from-red-500 to-pink-600' },
    { id: 'maintain', title: 'Manter Peso', description: 'Manter peso atual com alimentação equilibrada', icon: Heart, color: 'from-green-500 to-emerald-600' },
    { id: 'gain-muscle', title: 'Ganhar Massa', description: 'Aumentar massa muscular de forma saudável', icon: Activity, color: 'from-blue-500 to-indigo-600' }
  ]

  // diets e exercises seguem estrutura anterior

  return (
    <div className="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50 dark:from-slate-900 dark:to-slate-800">
      <Header />

      <div className="container mx-auto px-4 py-8 space-y-8">
        {/* Goals */}
        <section>
          <div className="text-center mb-8">
            <h2 className="text-3xl font-bold text-gray-900 dark:text-gray-100 mb-4">Qual é o seu objetivo?</h2>
            <p className="text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
              Escolha seu objetivo principal para receber recomendações personalizadas
            </p>
          </div>
          <div className="grid md:grid-cols-3 gap-6 mb-8">
            {goals.map(goal => (
              <GoalCard
                key={goal.id}
                {...goal}
                selected={selectedGoal === goal.id}
                onSelect={setSelectedGoal}
              />
            ))}
          </div>
        </section>

        {/* Tabs de Dietas / Exercícios */}
        {selectedGoal && (
          <Tabs defaultValue="diets" className="space-y-8">
            <TabsList className="grid w-full grid-cols-2 max-w-md mx-auto">
              <TabsTrigger value="diets" className="flex items-center gap-2"><Utensils className="w-4 h-4"/> Dietas & Receitas</TabsTrigger>
              <TabsTrigger value="exercises" className="flex items-center gap-2"><Dumbbell className="w-4 h-4"/> Exercícios</TabsTrigger>
            </TabsList>

            <TabsContent value="diets" className="space-y-8">
              {/* DietCards aqui */}
            </TabsContent>

            <TabsContent value="exercises" className="space-y-8">
              {/* ExerciseCards aqui */}
            </TabsContent>
          </Tabs>
        )}

        {/* Success Message */}
        {selectedGoal && selectedDiet && (
          <Card className="bg-gradient-to-r from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20 border-green-200 dark:border-green-800">
            <CardContent className="p-6 flex items-center gap-4">
              <div className="p-3 bg-green-500 rounded-full">
                <Star className="w-6 h-6 text-white"/>
              </div>
              <div>
                <h4 className="font-bold text-green-800 dark:text-green-200 mb-1">Parabéns! Seu plano está pronto</h4>
                <p className="text-green-700 dark:text-green-300 text-sm">
                  Você escolheu seu objetivo e dieta. Agora é só começar sua jornada saudável!
                </p>
              </div>
            </CardContent>
          </Card>
        )}
      </div>
    </div>
  )
}
