namespace RecipeApp1
{
    class Program
    {
        private static void Main(string[] args)
        {
            // Initialize a new recipe object
            Dictionary<string, Recipe> dictionaryRecipe = new Dictionary<string, Recipe>();
            Appmenu menu = new Appmenu(dictionaryRecipe);
            menu.appMenu();
        }
    }

    class recipeLogger
    {
        private Dictionary<string, Recipe> dictionaryRecipe;

        public recipeLogger(Dictionary<string, Recipe> dictionaryRecipe)
        {
            this.dictionaryRecipe = dictionaryRecipe;
        }

        public void loggerDetails()
        {
            // Prompt the user to enter the number of recipes
            Console.WriteLine("Enter the number of Recipe: ");
            int recipeNum;
            if (int.TryParse(Console.ReadLine(), out recipeNum))
            {
                for (int i = 0; i < recipeNum; i++)
                {
                    // Prompt the user to enter recipe details
                    Console.WriteLine("Enter Recipe ");
                    string recipeName = new Recipe().EnterData();
                    dictionaryRecipe.Add(recipeName, new Recipe());
                }

                // Prompt the user to display the recipe details
                string ans;
                do
                {
                    Console.WriteLine("Display Ingredient and Step?(Y/N)");
                    ans = Console.ReadLine();
                    switch (ans)
                    {
                        case "Y":
                            foreach (var recipeEntry in dictionaryRecipe)
                            {
                                Console.WriteLine($"Recipe Name: {recipeEntry.Key}");
                                recipeEntry.Value.RecipeDisplay();
                            }
                            break;
                        case "N":
                            Appmenu menu = new Appmenu(dictionaryRecipe);
                            menu.appMenu();
                            break;
                        default:
                            Console.WriteLine("Please enter a valid input");
                            break;
                    }
                } while (ans != "N");
            }
            else
            {
                Console.WriteLine("Please enter a number");
            }
        }

        public void recipeList()
        {
            foreach (var recipeEntry in dictionaryRecipe)
            {
                Console.WriteLine($"Recipe Name: {recipeEntry.Key}");
            }
        }

        public void recipeFinder()
        {
            Console.WriteLine("Please enter the name of the Recipe");
            string recipeName = Console.ReadLine();

            if (dictionaryRecipe.ContainsKey(recipeName))
            {
                Console.WriteLine($"Recipe Name: {recipeName}");
                dictionaryRecipe[recipeName].RecipeDisplay();
            }
            else
            {
                Console.WriteLine("Recipe does not exist");
            }
        }
    }

    class ingredientMenu
    {
        private Dictionary<string, Recipe> dictionaryRecipe;
        private object calories;

        public ingredientMenu(Dictionary<string, Recipe> dictionaryRecipe, object calories)
        {
            this.dictionaryRecipe = dictionaryRecipe;
            while (true)
            {
                // Display the menu options
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|WELCOME USER TO YOUR RECIPE MANGER APP....PLEASE SELECT A NUMBER");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 1 To Enter Recipe Details");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 2 To Display Menu");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 3 To Scale Recipes");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 4 To Rest Qauntity");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 5 To Clear Recipes");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 6 To Go Back To Main Menu");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 7 To Exit");
                Console.WriteLine("|=======================================================================|");
                string ans = Console.ReadLine();
                switch (ans)
                {
                    case "1":
                        //This line writes a message to the console, prompting the user to enter recipe details.
                        new Recipe().EnterData();
                        // Prompt the user to enter the number of ingredients
                        Console.WriteLine("|-----------------------------------------------------------------------|");
                        Console.WriteLine("|Enter Number Of Ingredients");
                        Console.WriteLine("|-----------------------------------------------------------------------|");
                        // Read user input
                        int ingNum = Convert.ToInt32(Console.ReadLine());
                        Console.WriteLine("|=======================================================================|");

                        // Initialize arrays with the specified size
                        new Recipe().ingrediants = new string[ingNum];
                        new Recipe().amount = new double[ingNum];
                        new Recipe().units = new string[ingNum];
                        new Recipe().calories = new double[ingNum];
                        new Recipe().foodGroup = new string[ingNum];

                        // Prompt the user to enter ingredient details
                        for (int i = 0; i < ingNum; i++)
                        {
                            // Prompt the user to enter the ingredient name
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            Console.WriteLine($"|Enter Ingredients Details# {i + 1}: ");
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            Console.WriteLine("|Name: ");
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            // Read user input
                            new Recipe().ingrediants[i] = Console.ReadLine();
                            Console.WriteLine("|=======================================================================|");

                            // Prompt the user to enter the ingredient quantity
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            //this will appear if the use input is wrong
                            do
                            {
                                Console.WriteLine("|Quantiy: ");
                            } while (!double.TryParse(Console.ReadLine(), out new Recipe().amount[i]));
                            Console.WriteLine("|-----------------------------------------------------------------------|");

                            // Prompt the user to enter the ingredient units
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            Console.WriteLine("|Units of Measurement: ");
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            new Recipe().units[i] = Console.ReadLine();
                            Console.WriteLine("|=======================================================================|");

                            // Prompt the user to enter the number of calories
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            //this will appear if the use input is wrong
                            do
                            {
                                Console.WriteLine("|Number of Calories: ");
                            } while (!double.TryParse(Console.ReadLine(), out new Recipe().calories[i]));
                            Console.WriteLine("|-----------------------------------------------------------------------|");

                            // Prompt the user to enter the food group
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            Console.WriteLine("|Enter Food Group: ");
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            new Recipe().foodGroup[i] = Console.ReadLine();
                        }

                        // Delegate double calExceed = callTotal(calories);
                        double calExceed = calTotal(calories);
                        Console.WriteLine("TOTAL CALORIES " + calExceed);
                        if (calExceed > 300)
                        {
                            Console.WriteLine("!!!TOTAL CALORIES EXCEED 300!!! ");
                        }


                        // Prompt the user to enter the number of steps
                        Console.WriteLine("|-----------------------------------------------------------------------|");
                        Console.WriteLine("|Enter Number of steps: ");
                        Console.WriteLine("|-----------------------------------------------------------------------|");

                        // Initialize arrays with the specified size
                        int stpNum = 0;

                        new Recipe().steps = new string[stpNum];

                        // Prompt the user to enter step details
                        for (int a = 0; a < stpNum; a++)
                        {
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            Console.WriteLine($"|Steps#{a + 1}: ");
                            Console.WriteLine("|-----------------------------------------------------------------------|");
                            new Recipe().steps[a] = Console.ReadLine();
                            Console.WriteLine("|=======================================================================|");
                        }
                        break;
                    case "2":
                        //This line writes a message to the console, prompting the user to display the menu
                        new Recipe().RecipeDisplay();
                        break;
                    case "3":
                        //This line writes a message to the console, prompting the user to scale the recipe
                        Console.WriteLine("Enter a scale of 0.5, 2 or 3");
                        double scale1 = Convert.ToDouble(Console.ReadLine());
                        new Recipe().RecipesScale(scale1);
                        break;
                    case "4":
                        // This line writes a message to the console, prompting the user to enter quantities.
                        new Recipe().RestRecipe();
                        break;
                    case "5":
                        //This line writes a message to the console, prompting the user to rest the recipe
                        new Recipe().ClearRecipe();
                        break;
                    case "6":
                        //This line writes a message to the console, prompting the user to rest the recipe
                        Appmenu menu = new Appmenu(dictionaryRecipe);
                        menu.appMenu();
                        break;
                    case "7":
                        // This line writes a message to the console, prompting the user to exit the program.
                        Environment.Exit(0);
                        break;
                    default:
                        Console.WriteLine("Wrong Vaild.Try Again");
                        break;
                }
            }

            this.calories = calories;
        }

        private double calTotal(object calories)
        {
            throw new NotImplementedException();
        }
    }

    class Recipe
    {
        // Declare private fields for ingredients, amounts, units, and steps
        public string[] ingrediants;
        public double[] amount;
        public string[] units;
        public string[] steps;
        private string recipeName;
        private string recipeDescription;
        public double[] calories;
        public string[] foodGroup;


        public Recipe()
        {
        }

        // EnterData method to enter recipe details
        public string EnterData()
        {
            Console.WriteLine("Enter Recipe Name: ");
            recipeName = Console.ReadLine();
            Console.WriteLine("Enter Recipe Description: ");
            recipeDescription = Console.ReadLine();
            return recipeName;
        }

        // Calculate the calories
        public double callTotal(double[] calories)
        {
            double result = 0;
            for (int i = 0; i < calories.Length; i++)
            {
                result += calories[i];
            }
            return result;
        }

        // RecipeDisplay method to display recipe details
        public void RecipeDisplay()
        {
            Console.WriteLine("Recipe Name: " + recipeName);
            Console.WriteLine("Recipe Description: " + recipeDescription);

            // Display the ingredients
            for (int i = 0; i < ingrediants.Length; i++)
            {
                Console.WriteLine("Ingredient " + (i + 1) + ": " + ingrediants[i] + " " + amount[i] + " " + units[i]);
            }

            // Display the steps
            for (int i = 0; i < steps.Length; i++)
            {
                Console.WriteLine("Step " + (i + 1) + ": " + steps[i]);
            }

            // Calculate the calories
            double result = 0;
            for (int i = 0; i < calories.Length; i++)
            {
                result += calories[i];
            }
            if (result > 300)
            {
                Console.WriteLine("!!!TOTAL CALORIES EXCEED 300!!! ");
            }
        }

        // RecipesScale method will increase amount
        public void RecipesScale(double scale)
        {
            for (int i = 0; i < amount.Length; i++)
            {
                amount[i] *= scale;
            }
        }

        // RestRecipe method will rest the amount to the original amount
        public void RestRecipe()
        {
            for (int i = 0; i < amount.Length; i++)
            {
                amount[i] /= 2;
            }
        }

        // ClearRecipe will clear all the array
        public void ClearRecipe()
        {
            // Declaring the array to null
            ingrediants = null;
            amount = null;
            units = null;
            steps = null;
        }
    }

    class Appmenu
    {
        public void appMenu()
        { }
        private Dictionary<string, Recipe> dictionaryRecipe;
        private recipeLogger repL;

        public Appmenu(Dictionary<string, Recipe> dictionaryRecipe)
        {
            this.dictionaryRecipe = dictionaryRecipe;
            repL = new recipeLogger(dictionaryRecipe);
        }

        public void appMenu(Recipe recipe)
        {
            while (true)
            {
                // Display the menu options
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|WELCOME USER TO YOUR RECIPE MANGER APP....PLEASE SELECT A NUMBER");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 1 To Create Recipe");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 2 To Search For Recipe");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 3 To Display All Recipes");
                Console.WriteLine("|=======================================================================|");
                Console.WriteLine("|Enter 4 Exit");
                Console.WriteLine("|=======================================================================|");
                string ans = Console.ReadLine();
                switch (ans)
                {
                    case "1":
                        repL.loggerDetails();
                        break;
                    case "2":
                        repL.recipeFinder();
                        break;
                    case "3":
                        repL.recipeList();
                        break;
                    case "4":
                        Environment.Exit(0);
                        break;
                    default:
                        Console.WriteLine("Wrong Vaild.Try Again");
                        break;
                }
            }
        }
    }
}
