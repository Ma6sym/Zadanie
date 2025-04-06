class Produkt
{
    public string Nazwa { get; set; }
    public int Ilosc { get; set; }
    public double Cena { get; set; }


    public Produkt(string nazwa, int ilosc, double cena)
    {
        Nazwa = nazwa;
        Ilosc = ilosc;
        Cena = cena;
    }
}
class Program
{
    static List<Produkt> magazyn = new List<Produkt>();
    private static string nazwa;

    static void Main()
    {
        while (true)
        {
            Console.WriteLine("\nWybierz opcje:");
            Console.WriteLine("1.Dodaj produkt");
            Console.WriteLine("2.Usuń produkt");
            Console.WriteLine("3.Wyświetl listę produktów");
            Console.WriteLine("4.Aktualizuj produkt");
            Console.WriteLine("5.Oblicz wartość magazynu");
            Console.WriteLine("6.Wyjście");
=
            string opcja = Console.ReadLine();
            switch (opcja)
            {
                case "1":
                    DodajProdukt();
                    break;
                case "2":
                    UsunProdukt();
                    break;
                case "3":
                    WyswietlProdukty();
                    break;
                case "4":
                    AktualizujProdukt();
                    break;
                case "5":
                    ObliczWartoscMagazynu();
                    break;
                case "6":
                    return;
                default:
                    Console.WriteLine("Nieprawidłowa opcja, spróbuj ponownie.");
                    break;
            }
        }
    }

    
    static void DodajProdukt()
    {
        Console.WriteLine("Podaj nazwe produktu: ");
        string nazwa = Console.ReadLine();

        Console.WriteLine("Podaj ilość: ");
        int ilosc = Convert.ToInt32(Console.ReadLine());

        Console.Write("Podaj cenę jednostkową: ");
        double cena = Convert.ToDouble(Console.ReadLine());

        magazyn.Add(new Produkt(nazwa, ilosc, cena));
        Console.WriteLine("produkt dodany!");
    }

    static void UsunProdukt()
    {
        Console.WriteLine("podaj nazwe produktu do usunięcia:");
        string nazwa = Console.ReadLine();
        Produkt produkt = magazyn.Find(p => p.Nazwa == nazwa);


        if (produkt != null)
        {
            magazyn.Remove(produkt);
            Console.WriteLine("produkt usunięty!");
        }

        else
        {
            Console.WriteLine("Produkt nie został znaleziony.");
        }
    }

    static void WyswietlProdukty()
    {
        Console.WriteLine("\nLista produktów w magazynie:");
        foreach (var Produkt in magazyn)
        {
            Console.WriteLine($"Nazwa: {Produkt.Nazwa}, Ilosc: {Produkt.Ilosc}, Cena: {Produkt.Cena:C}");
        }
    }

    static void AktualizujProdukt()
    {
        Console.WriteLine("Podaj nazwe produktu do aktualizacji: ");
        string nowailosc = Console.ReadLine();
        Produkt produkt = magazyn.Find(p => p.Nazwa == nazwa);

        if (produkt != null)
        {
            Console.Write("Podaj nową ilość (pozostaw puste, jeśli bez zmian): ");
            string nowaIlosc = Console.ReadLine();
            if (!string.IsNullOrEmpty(nowaIlosc))
                produkt.Ilosc = Convert.ToInt32(nowaIlosc);

            Console.Write("Podaj nową cenę jednostkową (pozostaw puste, jeśli bez zmian): ");
            string nowaCena = Console.ReadLine();
            if (!string.IsNullOrEmpty(nowaCena))
                produkt.Cena = Convert.ToDouble(nowaCena);

            Console.WriteLine("produkt zaktualizowany!");
        }
        else
        {
            Console.WriteLine("Produkt nie znaleziony.");
        }
    }

    static void ObliczWartoscMagazynu()
    {
        double wartosc = 0;
        foreach (var produkt in magazyn)
        {
            wartosc += produkt.Ilosc * produkt.Cena;
        }
        Console.WriteLine($"całkowita wartość magazynu: {wartosc:C}");
    }
}




