// Kod do projektu

    using System;
    using System.IO;

    namespace AplikacjaSzkoleniowa
    {

    class Program
    {
    
        // Klasa reprezentująca uczestnika szkolenia
        public class Uczestnik
        {
            public string Imie { get; set; }
            public string Nazwisko { get; set; }
            public string Adres { get; set; }
        }
        
        // Klasa reprezentująca kurs
        public class Kurs
        {
            public string NazwaKursu { get; set; }
            public DateTime DataRozpoczecia { get; set; }
            public int CzasTrwaniaDni { get; set; }
            public string Opis { get; set; }
        }

        // Klasa reprezentująca szkolenie
        public class Szkolenie
        {
            public Uczestnik Uczestnik { get; set; }
            public Kurs Kurs { get; set; }
        }

        // Funkcja do zbierania danych z konsoli
        public static Szkolenie ZbierzDaneZKonsoli()
        {
            var uczestnik = new Uczestnik();
            Console.WriteLine("Wprowadź dane uczestnika:");
            Console.Write("Imię: ");
            uczestnik.Imie = Console.ReadLine();
            Console.Write("Nazwisko: ");
            uczestnik.Nazwisko = Console.ReadLine();
            Console.Write("Adres zamieszkania: ");
            uczestnik.Adres = Console.ReadLine();

            var kurs = new Kurs();
            Console.WriteLine("Wprowadź dane kursu:");
            Console.Write("Nazwa kursu: ");
            kurs.NazwaKursu = Console.ReadLine();
            Console.Write("Data rozpoczęcia (yyyy-mm-dd): ");
            kurs.DataRozpoczecia = DateTime.Parse(Console.ReadLine());
            Console.Write("Czas trwania w dniach: ");
            kurs.CzasTrwaniaDni = int.Parse(Console.ReadLine());
            Console.Write("Opis kursu: ");
            kurs.Opis = Console.ReadLine();

            return new Szkolenie { Uczestnik = uczestnik, Kurs = kurs };
        }

        // Funkcja do zbierania danych z pliku
        public static Szkolenie ZbierzDaneZPliku(string sciezkaPliku)
        {
            var linie = File.ReadAllLines(sciezkaPliku);
            var uczestnik = new Uczestnik
            {
                Imie = linie[0],
                Nazwisko = linie[1],
                Adres = linie[2]
            };
            var kurs = new Kurs
            {
                NazwaKursu = linie[3],
                DataRozpoczecia = DateTime.Parse(linie[4]),
                CzasTrwaniaDni = int.Parse(linie[5]),
                Opis = linie[6]
            };
            return new Szkolenie { Uczestnik = uczestnik, Kurs = kurs };
        }

        static void Main(string[] args)
        {
            Console.WriteLine("Wybierz sposób wprowadzania danych:");
            Console.WriteLine("1. Konsola");
            Console.WriteLine("2. Plik tekstowy");
            var wybor = Console.ReadLine();

            Szkolenie szkolenie;
            if (wybor == "1")
            {
                szkolenie = ZbierzDaneZKonsoli();
            }
            else if (wybor == "2")
            {
                Console.Write("Podaj ścieżkę do pliku: ");
                var sciezkaPliku = Console.ReadLine();
                szkolenie = ZbierzDaneZPliku(sciezkaPliku);
            }
            else
            {
                Console.WriteLine("Nieprawidłowy wybór.");
                return;
            }

            Console.WriteLine("Dane szkolenia:");
            Console.WriteLine($"Uczestnik: {szkolenie.Uczestnik.Imie} {szkolenie.Uczestnik.Nazwisko}, {szkolenie.Uczestnik.Adres}");
            Console.WriteLine($"Kurs: {szkolenie.Kurs.NazwaKursu}, Data rozpoczęcia: {szkolenie.Kurs.DataRozpoczecia}, Czas trwania: {szkolenie.Kurs.CzasTrwaniaDni} dni, Opis: {szkolenie.Kurs.Opis}");
        }
    }
    }
