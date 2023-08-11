```c#
List<string> TaskList = new List<string>(); // De inicializar la clase pasa a ser una variable
int menuSelected = 0;
do
{
    menuSelected = ShowMainMenu();
    if ((Menu)menuSelected == Menu.Add) // Cambio automatico del menuSelected
    {
        ShowMenuAdd();
    }
    else if ((Menu)menuSelected == Menu.Remove)
    {
        ShowMenuRemove();
    }
    else if ((Menu)menuSelected == Menu.List)
    {
        ShowMenuTaskList();
    }
} while ((Menu)menuSelected != Menu.Exit);

/// <summary>
/// Show the main menu 
/// </summary>
/// <returns>Returns option indicated by user</returns>
int ShowMainMenu()
{
    Console.WriteLine("----------------------------------------");
    Console.WriteLine("Ingrese la opción a realizar: ");
    Console.WriteLine("1. Nueva tarea");
    Console.WriteLine("2. Remover tarea");
    Console.WriteLine("3. Tareas pendientes");
    Console.WriteLine("4. Salir");

    // Read line
    try
    {
        string selectedOption = Console.ReadLine();
        return Convert.ToInt32(selectedOption);
    }
    catch (Exception)
    {
        Console.WriteLine("Opción inválida, ingresa un valor dentro de las opciones.");
        return -1;
    }

}
void ShowMenuRemove()
{
    try
    {
        Console.WriteLine("Ingrese el número de la tarea a remover: ");
        // Show current taks
        ListOfTasks(); // Invocamos el codigo de la función para no repetir DRY

        string selectedOption = Console.ReadLine();
        // Remove one position
        int indexToRemove = Convert.ToInt32(selectedOption) - 1;

        // Controll the number insert for the user in the list
        if (indexToRemove > (TaskList.Count - 1) || indexToRemove < 0) // Si se ingresa un numero mayor a la cantidad de elementos.
        {
            Console.WriteLine("El número de tarea seleccionado no es válido, esta fuera de rango");
        }
        else
        {
            if (indexToRemove > -1 && TaskList.Count > 0)
            {
                string taskToRemove = TaskList[indexToRemove];
                TaskList.RemoveAt(indexToRemove);
                Console.WriteLine($"Tarea {taskToRemove} eliminada");  // Se interpola la cadena  
            }
        }

    }
    catch (Exception) // Catch teh exception 
    {
        Console.WriteLine("Ha ocurrido algun error al eliminar la tarea");

    }
}

void ShowMenuAdd()
{
    try
    {
        Console.WriteLine("Ingrese el nombre de la tarea: ");
        string task = Console.ReadLine();
        TaskList.Add(task);
        Console.WriteLine("Tarea registrada");
    }
    catch (Exception)
    {
        Console.WriteLine("Error inesperado al captirar la tarea \n vuelve a intentar");
    }
}

void ShowMenuTaskList() // Metodo para mostrar las tareas
{
    if (TaskList?.Count > 0)
    /* Revisar si el dato es null, reviasar si el `Count` es mayor a 0. 
    Verificamos que la cantidad de registros sea mayor a 0, si task list es null
    */
    {
        ListOfTasks();
        Console.WriteLine("----------------------------------------");
    }
    else
    {
        Console.WriteLine("No hay tareas por realizar");
    }
}

void ListOfTasks()
{
    Console.WriteLine("----------------------------------------");
    var indexTask = 1;  // Declaramos la variable
    TaskList.ForEach(task => Console.WriteLine($"{indexTask++} . {task}")); // Expresión lamda, nos ayuda a ahacer el recorrido. // Se interpola la cadena

    Console.WriteLine("----------------------------------------");
}

public enum Menu // Numeration
{
    Add = 1,
    Remove = 2,
    List = 3,
    Exit = 4
}
```