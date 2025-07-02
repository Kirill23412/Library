# Library
Библиотека на C#
Класс Book:

   internal class Book
 {
     public string TitleBook { get; set; }
     public int col {  get; set; }
     public Book(string TitleBook)
     {
         this.TitleBook = TitleBook;
         this.col = 1;
        
     }

 }

 Класс Author:
   internal class Author
{
    public string Name { get; set; }
    public Author(string name)
    {
        this.Name = name;
    }
}

Класс Publication:Author:
   internal class Publication:Author
 {
     public int EditionNumber { get; set; }
     public int Year { get; set; }
     public Publication(string name, int editionNumber, int year) : base(name)
     {
         EditionNumber = editionNumber;
         Year = year;
     }
 }

 Класс Bible:
 
    internal class Bible
 {
     public int count = 0;
     private Book[] books;
     private int bookCount;
     private int readerCount;

     public Bible()
     {
         bookCount = 0;
         readerCount = 0;
     }

     public void BookInv(string TitleBook)
     {
         books[count] = new Book(TitleBook);
         count++;
         
     }
 }

 Класс Librian:
   internal class Librian
{
    public string Name { get; set; }

    public Librian(string name) {

        this.Name = name;
    
    }

}

Класс Reader:
  internal class Reader
{
    public int g = 0;

    public string FIO { get; set; }
    public int Age { get; set; }
    public int GetBook {  get; set; }
    public Reader(string fio, int age) {
    
        FIO = fio;
        Age = age;
        GetBook = 0;

    }

    public string ToString() {
    
        return $"имя:{FIO} возраст:{Age} взятых книг:{GetBook}";

    }
}

Файл Form1:
   public int g = 0;
 public int b = 0;
 Reader[] read = new Reader[100];
 Book[] bibles = new Book[100];
 Librian librian = new Librian("Владимир");

 public Form1()
 {
     

     InitializeComponent();
 }

 private void Form1_Load(object sender, EventArgs e)
 {

 }

 private void textBox1_TextChanged(object sender, EventArgs e)
 {

 }

 private void button1_Click(object sender, EventArgs e)
 {
     try
     {
         if (textBox1.Text != null && textBox2.Text != null)
         {
             string fio = textBox1.Text;
             int age = int.Parse(textBox2.Text);

             for (int i = 0; i < 1; i++)
             {
                 read[g] = new Reader(fio, age);
                 listBox1.Items.Add(fio);
             }
             g++;
             textBox1.Clear();
             textBox2.Clear();
         }
         else
         {

             MessageBox.Show("Введите что нибудь в поле ввода или введите коректные данные(числа вместо букв)");

         }
     }
     catch (Exception ex)
     {

         MessageBox.Show($"Произошла ошибка: {ex.Message}", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);
     }
 }

 private void label4_Click(object sender, EventArgs e)
 {

 }

 private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
 {

 }

 private void button2_Click(object sender, EventArgs e)
 {
     try
     {
         if (listBox1.SelectedItem != null)
         {
             MessageBox.Show(listBox1.SelectedItem.ToString());
         }
     }
     catch (Exception ex)
     {

         MessageBox.Show($"Произошла ошибка: {ex.Message}", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);
     }
 }

 private void button3_Click(object sender, EventArgs e)
 {
     try
     {
         string title = textBox3.Text;
         for (int i = 0; i < 1; i++)
         {
             bibles[b] = new Book(title);
             listBox2.Items.Add(title);
         }
         textBox3.Clear();
         b++;
     }
     catch (Exception ex)
     {

         MessageBox.Show($"Произошла ошибка: {ex.Message}", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);
     }
 }

 private void button4_Click(object sender, EventArgs e)
 {

     string names = textBox5.Text; 
     string Titles = textBox4.Text;

     if (!string.IsNullOrEmpty(names) && !string.IsNullOrEmpty(Titles))
     {
         bool bookFound = false; 
         bool personFound = false; 

         foreach (var titlee in bibles)
         {
             if (titlee != null && titlee.TitleBook.Equals(Titles, StringComparison.OrdinalIgnoreCase))
             {
                 bookFound = true; 

                 foreach (var person in read)
                 {
                     if (person.FIO.Equals(names, StringComparison.OrdinalIgnoreCase))
                     {
                         personFound = true; 

                         if (titlee.col > 0)
                         {
                             person.GetBook += 1; 
                             titlee.col -= 1; 
                             MessageBox.Show($"Книга {Titles} выдана {names}, библиотекарем {librian.Name}, всего книг у клиента - {person.GetBook}");
                         }
                         else
                         {
                             MessageBox.Show("Книг не хватает!");
                         }
                         break; 
                     }
                 }
                 break; 
             }
         }

  
         if (!bookFound)
         {
             MessageBox.Show("Книга не найдена.");
         }
         else if (!personFound)
         {
             MessageBox.Show("Человек не найден.");
         }
     }
     else
     {
         MessageBox.Show("Пожалуйста, введите имя и название книги.");
     }



 }



 private void textBox2_TextChanged(object sender, EventArgs e)
 {

 }

 private void textBox2_KeyPress(object sender, KeyPressEventArgs e)
 {
     if (!char.IsControl(e.KeyChar) && !char.IsDigit(e.KeyChar))
     {
         e.Handled = true;
     }
 }

 private void listBox2_SelectedIndexChanged(object sender, EventArgs e)
 {

 }

 private void textBox5_TextChanged(object sender, EventArgs e)
 {

 }

 private void button5_Click(object sender, EventArgs e)
 {

 }

 private void button5_Click_1(object sender, EventArgs e)
 {
     try
     {
         string title = textBox3.Text;

         if (string.IsNullOrEmpty(title))
         {
             MessageBox.Show("Пожалуйста, введите название книги.");
             return;
         }

         bool found = false;

         foreach (var a in bibles)
         {
             if (a != null && a.TitleBook.Equals(title, StringComparison.OrdinalIgnoreCase))
             {
                 a.col += 1;
                 MessageBox.Show("Количество увеличено на 1 книгу.");
                 found = true;
                 break;
             }
         }

         if (!found)
         {
             MessageBox.Show("Книга не найдена.");
         }
     }
     catch (Exception ex)
     {

         MessageBox.Show($"Произошла ошибка: {ex.Message}", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Error);

     }
 }
![image](https://github.com/user-attachments/assets/4102e869-54e4-4eb6-a595-2612a90ff114)
