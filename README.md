
### **Билет 1**
> Написать программу, которая после введенного числа от 1 до 999 дописывает слово «рубль» в правильной форме.

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите число от 1 до 999: ");
        int n = int.Parse(Console.ReadLine());

        string[] forms = { "рубль", "рубля", "рублей" };
        int remainder = n % 100;
        if (remainder >= 11 && remainder <= 14)
            Console.WriteLine($"{n} рублей");
        else
        {
            switch (n % 10)
            {
                case 1: Console.WriteLine($"{n} рубль"); break;
                case 2:
                case 3:
                case 4: Console.WriteLine($"{n} рубля"); break;
                default: Console.WriteLine($"{n} рублей"); break;
            }
        }
    }
}
```

---

### **Билет 2**
> То же самое, но для слова «копейка»

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите число от 1 до 99: ");
        int n = int.Parse(Console.ReadLine());

        string[] forms = { "копейка", "копейки", "копеек" };
        int remainder = n % 100;
        if (remainder >= 11 && remainder <= 14)
            Console.WriteLine($"{n} копеек");
        else
        {
            switch (n % 10)
            {
                case 1: Console.WriteLine($"{n} копейка"); break;
                case 2:
                case 3:
                case 4: Console.WriteLine($"{n} копейки"); break;
                default: Console.WriteLine($"{n} копеек"); break;
            }
        }
    }
}
```

---

### **Билет 3**
> Программа выводит пример на вычитание, проверяет ответ пользователя.

```csharp
using System;

class Program
{
    static void Main()
    {
        Random rand = new Random();
        int a = rand.Next(1, 100);
        int b = rand.Next(1, a); // чтобы не было отрицательных

        Console.WriteLine($"Сколько будет {a} - {b}?");

        int answer = int.Parse(Console.ReadLine());

        if (answer == a - b)
            Console.WriteLine("Правильно!");
        else
            Console.WriteLine($"Вы ошиблись! Правильный ответ: {a - b}");
    }
}
```

---

### **Билет 4**
> Преобразование десятичного числа (0–255) в двоичное

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите число от 0 до 255: ");
        int n = int.Parse(Console.ReadLine());

        string binary = Convert.ToString(n, 2).PadLeft(8, '0');
        Console.WriteLine($"Двоичное представление: {binary}");
    }
}
```

---

### **Билет 5**
> Процедура `TrianglePS(a, P, S)` для равностороннего треугольника

```csharp
using System;

class Program
{
    static void TrianglePS(double a, out double P, out double S)
    {
        P = 3 * a;
        S = (Math.Pow(a, 2) * Math.Sqrt(3)) / 4;
    }

    static void Main()
    {
        double a, P, S;
        for (int i = 1; i <= 3; i++)
        {
            Console.Write($"Введите сторону треугольника {i}: ");
            a = double.Parse(Console.ReadLine());
            TrianglePS(a, out P, out S);
            Console.WriteLine($"Периметр: {P:F2}, Площадь: {S:F2}");
        }
    }
}
```

---

### **Билет 6**
> Матрица M x N, поменять левую нижнюю и правую верхнюю четверти

```csharp
using System;

class Program
{
    static void Main()
    {
        int[,] matrix = {
            {1, 2, 3, 4},
            {5, 6, 7, 8},
            {9, 10, 11, 12},
            {13, 14, 15, 16}
        };

        int m = matrix.GetLength(0), n = matrix.GetLength(1);

        int halfM = m / 2, halfN = n / 2;

        for (int i = halfM; i < m; i++)
        {
            for (int j = 0; j < halfN; j++)
            {
                int temp = matrix[i, j];
                matrix[i, j] = matrix[i - halfM, j + halfN];
                matrix[i - halfM, j + halfN] = temp;
            }
        }

        PrintMatrix(matrix);
    }

    static void PrintMatrix(int[,] mat)
    {
        for (int i = 0; i < mat.GetLength(0); i++)
        {
            for (int j = 0; j < mat.GetLength(1); j++)
                Console.Write(mat[i, j] + "\t");
            Console.WriteLine();
        }
    }
}
```

---

### **Билет 7**
> Поворот матрицы на 90° против часовой стрелки

```csharp
using System;

class Program
{
    static void RotateMatrix(int[,] mat)
    {
        int n = mat.GetLength(0);
        for (int layer = 0; layer < n / 2; layer++)
        {
            int first = layer;
            int last = n - layer - 1;
            for (int i = first; i < last; i++)
            {
                int offset = i - first;
                int top = mat[first, i];
                mat[first, i] = mat[i, last];
                mat[i, last] = mat[last, last - offset];
                mat[last, last - offset] = mat[last - offset, first];
                mat[last - offset, first] = top;
            }
        }
    }

    static void Main()
    {
        int[,] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        RotateMatrix(matrix);
        PrintMatrix(matrix);
    }

    static void PrintMatrix(int[,] mat)
    {
        for (int i = 0; i < mat.GetLength(0); i++)
        {
            for (int j = 0; j < mat.GetLength(1); j++)
                Console.Write(mat[i, j] + "\t");
            Console.WriteLine();
        }
    }
}
```

---

### **Билет 8**
> Вывести элементы массива с четными номерами и нечетными в обратном порядке

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] arr = {1, 2, 3, 4, 5, 6};

        Console.WriteLine("Четные позиции:");
        for (int i = 0; i < arr.Length; i += 2)
            Console.Write(arr[i] + " ");

        Console.WriteLine("\nНечетные позиции в обратном порядке:");
        for (int i = arr.Length - 1; i >= 0; i -= 2)
            Console.Write(arr[i] + " ");
    }
}
```

---

### **Билет 9**
> Шифрование строки циклической заменой букв

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите строку: ");
        string input = Console.ReadLine();

        string result = "";
        foreach (char c in input)
        {
            if (c >= 'А' && c < 'Я') result += (char)(c + 1);
            else if (c == 'Я') result += 'А';
            else if (c >= 'а' && c < 'я') result += (char)(c + 1);
            else if (c == 'я') result += 'а';
            else result += c;
        }

        Console.WriteLine("Зашифрованная строка: " + result);
    }
}
```

---

### **Билет 10**
> Расчет вклада с увеличением на проценты

```csharp
using System;

class Program
{
    static void Main()
    {
        double deposit = 1000;
        Console.Write("Введите процент (например, 5): ");
        double percent = double.Parse(Console.ReadLine());
        int months = 0;

        while (deposit <= 1100)
        {
            deposit *= (1 + percent / 100);
            months++;
        }

        Console.WriteLine($"Количество месяцев: {months}");
        Console.WriteLine($"Итоговая сумма: {deposit:F2}");
    }
}
```

---

---

### **Билет 11**
> Написать программу, которая вычисляет число π с заданной точностью через ряд:  
> `π/4 = 1 - 1/3 + 1/5 - 1/7 + ...`

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите количество членов ряда: ");
        int n = int.Parse(Console.ReadLine());

        double pi = 0;
        for (int i = 0; i < n; i++)
        {
            double term = Math.Pow(-1, i) / (2 * i + 1);
            pi += term;
        }

        pi *= 4;
        Console.WriteLine($"Число π ≈ {pi:F10}");
    }
}
```

---

### **Билет 12**
> Программа «Скидка»: рассчитывает стоимость покупки с учетом скидки (>1000 руб.) и выходных дней.

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите сумму покупки: ");
        double sum = double.Parse(Console.ReadLine());

        bool isWeekend = DateTime.Now.DayOfWeek == DayOfWeek.Saturday ||
                         DateTime.Now.DayOfWeek == DayOfWeek.Sunday;

        if (sum > 1000 || isWeekend)
        {
            sum *= 0.95; // 5% скидка
            Console.WriteLine("Скидка применена.");
        }
        else
        {
            Console.WriteLine("Скидка не применяется.");
        }

        Console.WriteLine($"Итоговая сумма: {sum:F2} руб.");
    }
}
```

---

### **Билет 13**
> Программа "Колледж" с БД студентов и родителей (3 записи), вывод в формах.

#### Используем:
- **Visual Studio** + **WinForms**
- **SQLite** / **SQL Server**

##### Пример структуры базы:

```sql
CREATE TABLE Students (
    Id INTEGER PRIMARY KEY AUTOINCREMENT,
    Name TEXT,
    GroupName TEXT
);

CREATE TABLE Parents (
    Id INTEGER PRIMARY KEY AUTOINCREMENT,
    StudentId INTEGER,
    Name TEXT,
    FOREIGN KEY(StudentId) REFERENCES Students(Id)
);
```

В приложении используйте **DataGridView**, **DataAdapter**, **DataSet** для отображения данных.

---

### **Билет 14**
> Программа "Магазин" — аналогично предыдущему, но с товарами и покупателями.

Такая же реализация, только таблицы:

- `Products`
- `Customers`
- `Sales` (связь между ними)

---

### **Билет 15**
> Программа "Аэропорт" — рейсы и пассажиры.

Таблицы:

- `Flights`
- `Passengers`
- `Tickets`

Реализация через WinForms + DataGridView

---

### **Билет 16**
> Расчет стоимости поездки на автомобиле

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите расход топлива на 100 км: ");
        double fuelRate = double.Parse(Console.ReadLine());
        Console.Write("Введите цену литра бензина: ");
        double pricePerLiter = double.Parse(Console.ReadLine());
        Console.Write("Введите расстояние: ");
        double distance = double.Parse(Console.ReadLine());

        double cost = (fuelRate / 100) * distance * pricePerLiter;
        Console.WriteLine($"Стоимость поездки: {cost:F2} руб.");
    }
}
```

---

### **Билет 17**
> Расчет стоимости окна (стеклопакета)

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите ширину окна (м): ");
        double width = double.Parse(Console.ReadLine());
        Console.Write("Введите высоту окна (м): ");
        double height = double.Parse(Console.ReadLine());

        double area = width * height;
        double pricePerSquareMeter = 3000; // цена за м²

        double total = area * pricePerSquareMeter;
        Console.WriteLine($"Стоимость окна: {total:F2} руб.");
    }
}
```

---

### **Билет 18**
> Калькулятор (+, -, *, /)

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите первое число: ");
        double a = double.Parse(Console.ReadLine());
        Console.Write("Введите операцию (+, -, *, /): ");
        char op = Console.ReadKey().KeyChar;
        Console.WriteLine();
        Console.Write("Введите второе число: ");
        double b = double.Parse(Console.ReadLine());

        switch (op)
        {
            case '+': Console.WriteLine(a + b); break;
            case '-': Console.WriteLine(a - b); break;
            case '*': Console.WriteLine(a * b); break;
            case '/': Console.WriteLine(b != 0 ? a / b : "Ошибка: деление на ноль"); break;
            default: Console.WriteLine("Неверная операция"); break;
        }
    }
}
```

---

### **Билет 19**
> Программа "Магазин товаров" с уменьшением количества

```csharp
using System;

class Program
{
    static void Main()
    {
        string[] products = { "Хлеб", "Молоко", "Яйца" };
        int[] quantities = { 10, 5, 15 };

        while (true)
        {
            Console.WriteLine("Выберите товар:");
            for (int i = 0; i < products.Length; i++)
                Console.WriteLine($"{i + 1}. {products[i]} – {quantities[i]} шт.");

            Console.Write("Введите номер товара (или 0 для выхода): ");
            int choice = int.Parse(Console.ReadLine()) - 1;

            if (choice == -1) break;
            if (choice >= 0 && choice < products.Length && quantities[choice] > 0)
            {
                quantities[choice]--;
                Console.WriteLine("Куплено!");
            }
            else
            {
                Console.WriteLine("Нет в наличии");
            }
        }
    }
}
```

---

### **Билет 20**
> Расчет коммунальных услуг (электроэнергия)

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Введите начальное показание счетчика: ");
        double start = double.Parse(Console.ReadLine());
        Console.Write("Введите конечное показание счетчика: ");
        double end = double.Parse(Console.ReadLine());
        Console.Write("Введите тариф за кВт·ч: ");
        double rate = double.Parse(Console.ReadLine());

        double consumption = end - start;
        double cost = consumption * rate;
        Console.WriteLine($"Сумма к оплате: {cost:F2} руб.");
    }
}
```

---

### **Билет 21**
> Часы с фоном в зависимости от времени суток

Реализуется через **WPF** или **WinForms** с `Timer`, меняющим изображение фона в зависимости от часа.

```xaml
<!-- WPF -->
<Window x:Class="ClockApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Grid>
        <Image x:Name="BackgroundImage"/>
        <TextBlock x:Name="TimeText" FontSize="36" HorizontalAlignment="Center" VerticalAlignment="Center"/>
    </Grid>
</Window>
```

```csharp
// MainWindow.xaml.cs
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
        var timer = new DispatcherTimer { Interval = TimeSpan.FromSeconds(1) };
        timer.Tick += Timer_Tick;
        timer.Start();
    }

    private void Timer_Tick(object sender, EventArgs e)
    {
        var now = DateTime.Now;
        TimeText.Text = now.ToString("HH:mm:ss");

        string bg = now.Hour switch
        {
            >= 5 and < 12 => "morning.jpg",
            >= 12 and < 18 => "day.jpg",
            _ => "night.jpg"
        };

        BackgroundImage.Source = new BitmapImage(new Uri(bg, UriKind.Relative));
    }
}
```

---

### **Билет 22**
> Анимация кораблика

Реализуется через **GDI+** в WinForms или **Canvas + Animation** в WPF.

Пример:

```csharp
private int shipX = 0;

private void timer1_Tick(object sender, EventArgs e)
{
    shipX += 5;
    if (shipX > ClientSize.Width) shipX = -100;
    Invalidate();
}

private void Form1_Paint(object sender, PaintEventArgs e)
{
    e.Graphics.FillEllipse(Brushes.Blue, shipX, 100, 50, 20); // корпус
    e.Graphics.FillPolygon(Brushes.Red, new Point[]
    {
        new(shipX + 20, 80),
        new(shipX + 25, 100),
        new(shipX + 30, 80)
    }); // парус
}
```

---

### **Билет 23**
> Программа "Экзаменатор"

Создается форма с вопросами, ответами, сохранением результата в файл.

```csharp
StreamWriter writer = File.AppendText("results.txt");
writer.WriteLine($"{DateTime.Now} - {username}: {score}/5");
writer.Close();
```

---

### **Билет 24**
> Определить количество дней в году (високосный?)

```csharp
Console.Write("Введите год: ");
int year = int.Parse(Console.ReadLine());

bool leap = (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
Console.WriteLine(leap ? "366 дней" : "365 дней");
```

---

## 📱 Билеты 25–33 (Java / Мобильная разработка)

> Эти билеты требуют использования **Android Studio** и **Java/Kotlin** или **.NET MAUI/Xamarin**

---

### **Билет 25–28**
> Все эти задачи на Java: проверка пароля, удаление символов, перевод в двоичную систему, рекурсивный ввод массива

Пример перевода числа в двоичную систему рекурсивно:

```java
public class BinaryConverter {
    public static void toBinary(int n) {
        if (n > 1) toBinary(n / 2);
        System.out.print(n % 2);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Введите число: ");
        int num = sc.nextInt();
        toBinary(num);
    }
}
```

---

### **Билеты 29–33**
> Мобильные приложения (.NET MAUI / Xamarin / Android Studio)

Пример MainActivity.java:

```xml
<!-- activity_main.xml -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:text="ФИО:"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

    <EditText
        android:id="@+id/editName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

    <Button
        android:text="Отправить"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="onSubmit"/>
</LinearLayout>
```

```java
public void onSubmit(View view) {
    EditText nameField = findViewById(R.id.editName);
    String name = nameField.getText().toString();
    Toast.makeText(this, "Привет, " + name, Toast.LENGTH_SHORT).show();
}
```

---

