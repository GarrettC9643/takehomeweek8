namespace Exercise_3_Employee_Management_System
{
    internal class Program
{
    static void Main(string[] args)
    {
        // Creating instances of different employee types
        Manager manager = new Manager("Alice", "General Manager", 8000, 2000);
        Engineer engineer = new Engineer("Bob", "Software Engineer", 6000, 500);
        Salesperson salesperson = new Salesperson("Charlie", "Sales Executive", 4000, 10, 500);

        // Adding employees to the list
        List<Employee> employees = new List<Employee> { manager, engineer, salesperson };

        // Calculating total monthly salary for all employees
        decimal totalSalary = 0;
        foreach (var employee in employees)
        {
            totalSalary += employee.CalculateSalary();
        }

        Console.WriteLine($"Total Monthly Salary for all employees: {totalSalary:C}");

        // Demonstrating promotions and bonuses
        manager.Promote("Senior Manager", 1000);
        salesperson.GiveBonus(300);

        Console.WriteLine("\nAfter promotions and bonuses:");
        foreach (var employee in employees)
        {
            Console.WriteLine($"{employee.Name} ({employee.Title}) earns {employee.CalculateSalary():C} per month.");
        }
    }

    public abstract class Employee
    {
        public string Name { get; set; }
        public string Title { get; set; }
        public decimal Salary { get; set; }

        public Employee(string name, string title, decimal salary)
        {
            Name = name;
            Title = title;
            Salary = salary;
        }

        // Abstract method to calculate salary, implemented in derived classes
        public abstract decimal CalculateSalary();

        // Method to promote an employee
        public virtual void Promote(string newTitle, decimal raise)
        {
            Title = newTitle;
            Salary += raise;
            Console.WriteLine($"{Name} has been promoted to {Title} with a raise of {raise:C}.");
        }

        // Method to give a bonus to an employee
        public virtual void GiveBonus(decimal bonus)
        {
            Salary += bonus;
            Console.WriteLine($"{Name} has received a bonus of {bonus:C}.");
        }
    }

    public class Manager : Employee
    {
        public decimal Bonus { get; set; }

        public Manager(string name, string title, decimal salary, decimal bonus)
            : base(name, title, salary)
        {
            Bonus = bonus;
        }

        public override decimal CalculateSalary()
        {
            return Salary + Bonus;
        }

        public override void Promote(string newTitle, decimal raise)
        {
            base.Promote(newTitle, raise);
            Console.WriteLine($"{Name} now receives a total salary of {CalculateSalary():C} (including bonus).");
        }
    }

    public class Engineer : Employee
    {
        public decimal Allowance { get; set; }

        public Engineer(string name, string title, decimal salary, decimal allowance)
            : base(name, title, salary)
        {
            Allowance = allowance;
        }

        public override decimal CalculateSalary()
        {
            return Salary + Allowance;
        }
    }

    public class Salesperson : Employee
    {
        public decimal CommissionRate { get; set; }
        public decimal SalesAmount { get; set; }

        public Salesperson(string name, string title, decimal salary, decimal commissionRate, decimal salesAmount)
            : base(name, title, salary)
        {
            CommissionRate = commissionRate;
            SalesAmount = salesAmount;
        }

        public override decimal CalculateSalary()
        {
            return Salary + (SalesAmount * CommissionRate / 100);
        }

        public override void GiveBonus(decimal bonus)
        {
            base.GiveBonus(bonus);
            Console.WriteLine($"{Name} now receives a commission-adjusted salary of {CalculateSalary():C}.");
        }
    }
}
