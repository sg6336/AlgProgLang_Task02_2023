using System;

class Program
{
    static void Main()
    {
        Console.Write("Enter the number of rows: ");
        int rows = int.Parse(Console.ReadLine());

        Console.Write("Enter the number of columns: ");
        int columns = int.Parse(Console.ReadLine());

        int[,] matrix = new int[rows, columns];
        Random random = new Random();

        // Fill the matrix with random numbers
        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < columns; j++)
            {
                matrix[i, j] = random.Next(101); // Generate random number from 0 to 100 (inclusive)
            }
        }

        // Print the matrix with highlighted main diagonal
        Console.WriteLine("Matrix:");
        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < columns; j++)
            {
                if (i == j)
                {
                    Console.ForegroundColor = ConsoleColor.Red; // Highlight the main diagonal
                }
                Console.Write(matrix[i, j] + " ");
                Console.ResetColor();
            }
            Console.WriteLine();
        }

        // Calculate and print the matrix trace
        int trace = 0;
        for (int i = 0; i < Math.Min(rows, columns); i++)
        {
            trace += matrix[i, i];
        }
        Console.WriteLine("Matrix trace: " + trace);

        // Print matrix elements in snail shell order
        Console.WriteLine("Snail shell order:");
        int top = 0, bottom = rows - 1, left = 0, right = columns - 1;
        while (top <= bottom && left <= right)
        {
            // Print top row
            for (int i = left; i <= right; i++)
            {
                Console.Write(matrix[top, i] + " ");
            }
            top++;

            // Print right column
            for (int i = top; i <= bottom; i++)
            {
                Console.Write(matrix[i, right] + " ");
            }
            right--;

            if (top <= bottom)
            {
                // Print bottom row
                for (int i = right; i >= left; i--)
                {
                    Console.Write(matrix[bottom, i] + " ");
                }
                bottom--;
            }

            if (left <= right)
            {
                // Print left column
                for (int i = bottom; i >= top; i--)
                {
                    Console.Write(matrix[i, left] + " ");
                }
                left++;
            }
        }
    }
}
