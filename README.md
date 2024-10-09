namespace Exercise_3_Employee_Management_System
{
    internal class Program
    {
        static void Main(string[] args)
        {
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

        }
        public class Manager : Employee
        {

        }
        public class Engineer : Employee
        {

        }
        public class Salesperson : Employee
        {

        }
        public interface SalaryCalc
        {
            void Calc();
        }
    }
}
