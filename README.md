# Practice_2_Velykorod_report_
# Завдання
1. Скопіювати віддалений репозиторій (зробити Fork) за наданим посиланням у власний акаунт на GitHub:
https://github.com/IlonaShevchenko/Practice_Linq_2024
У вашому акаунті на GitHub має з’явитися репозиторій-копія (fork).
2. Клонувати отриманий fork-репозиторій на власний комп’ютер.
3. Перевірити, що склонований проєкт запускається і виводить на екран тестове значення 13049 (це кількість всіх матчів збірних, які були проведені з 2010 року включно).
4. Ознайомитися зі структурою проєкту.
У проєкті наявний код:
− опис класу FootballGame, який описує футбольний матч (FootballGame.сs);
− у файлі Program.cs вже реалізований метод ReadFromFileJson(), який десеріалізаціє json-файл (data/results_2010.json) у колекцію List;
− також у файлі Program.cs повністю реалізований метод Main().
5. Необхідно реалізувати методи Query1(), Query2(), …, Query10(), а саме: за допомогою мови LINQ реалізувати запити, формулювання яких оформлені у вигляді коментарів до кожного методу.
Крім запиту мовою LINQ у кожному методі має бути реалізований вивід на екран результатів запиту (приклад оформлення виводу див. у файлі output.txt).
6. Після реалізації кожного методу QueryN() необхідно робити commit, вказуючи номер N реалізованого запиту.
7. Оформити Readme.md файл. Оформити звіт:
− Титульний аркуш
− Завдання
− Реалізація запитів
(навести формулювання запиту і його реалізацію за допомогою LINQ)
− Код програми
− Результат роботи програми
− Посилання на віддалений репозиторій студента
# ВИКОНАННЯ ЗАВДАННЯ
**Реалізація запитів**
```sh
    // Запит 1
    static void Query1(List<FootballGame> games)
    {
        //Query 1: Вивести всі матчі, які відбулися в Україні у 2012 році.

        var selectedGames = games.Where(g=>g.Country=="Ukraine"&& g.Date.Year==2012); // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 1 ========================");
        foreach(var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 2
    static void Query2(List<FootballGame> games)
    {
        //Query 2: Вивести Friendly матчі збірної Італії, які вона провела з 2020 року.  

        var selectedGames = games.Where(g=>g.Tournament=="Friendly"&&( g.Home_team=="Italy" || g.Away_team=="Italy")&& g.Date.Year >=2020); // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 2 ========================");
        foreach(var game in selectedGames )
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 3
    static void Query3(List<FootballGame> games)
    {
        //Query 3: Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.

        var selectedGames = games.Where(g=>g.Country=="France"&& g.Date.Year ==2021 && g.Home_score==g.Away_score) ;   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 3 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 4
    static void Query4(List<FootballGame> games)
    {
        //Query 4: Вивести всі матчі збірної Германії з 2018 року по 2020 рік (включно), в яких вона на виїзді програла.

        var selectedGames = games.Where(g=>g.Away_team=="Germany"&&g.Date.Year>=2018 && g.Date.Year <=2020 && g.Away_score<g.Home_score);   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 4 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }
    // Запит 5
    static void Query5(List<FootballGame> games)
    {
        //Query 5: Вивести всі кваліфікаційні матчі (UEFA Euro qualification), які відбулися у Києві чи у Харкові, а також за умови перемоги української збірної.
        var selectedGames = games.Where(g => g.Tournament == "UEFA Euro qualification" && (g.City == "Kyiv" || g.City =="Kharkiv")&&g.Home_team=="Ukraine"&&g.Home_score>g.Away_score);  // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 5 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 6
    static void Query6(List<FootballGame> games)
    {
        //Query 6: Вивести всі матчі останнього чемпіоната світу з футболу (FIFA World Cup), починаючи з чвертьфіналів (тобто останні 8 матчів).
        //Матчі мають відображатися від фіналу до чвертьфіналів (тобто у зворотній послідовності).
        var selectedGames = games.Where(g=>g.Tournament == "FIFA World Cup"&&g.Date.Year==2022).OrderByDescending(g=>g.Date).Take(8);   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 6 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 7
    static void Query7(List<FootballGame> games)
    {
        //Query 7: Вивести перший матч у 2023 році, в якому збірна України виграла.

        FootballGame g = games.Where(game => game.Date.Year == 2023 && 
        ((game.Home_team =="Ukraine"&& game.Home_score >game.Away_score) || 
        (game.Away_team == "Ukraine" && game.Away_score > game.Home_score)))
            .OrderBy(game=>game.Date)
            .FirstOrDefault();   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 7 ========================");
        if(g!=null)
        {
            Console.WriteLine($"{g.Date:dd.MM.yyyy} {g.Home_team} - {g.Away_team}, Score: {g.Home_score} - {g.Away_score}, Country: {g.Country}");
        }
        else { Console.WriteLine("No matches found."); }
    }

    // Запит 8
    static void Query8(List<FootballGame> games)
    {
        //Query 8: Перетворити всі матчі Євро-2012 (UEFA Euro), які відбулися в Україні, на матчі з наступними властивостями:
        // MatchYear - рік матчу, Team1 - назва приймаючої команди, Team2 - назва гостьової команди, Goals - сума всіх голів за матч

        var selectedGames = games.Where(g => g.Tournament == "UEFA Euro" && g.Date.Year == 2012 && g.Country == "Ukraine")
            .Select(g => new
            {
                MatchYear = g.Date.Year,
                Team1=g.Home_team ,
                Team2=g.Away_team ,
                Goals=g.Home_score+g.Away_score
            });   // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 8 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.MatchYear} {game.Team1} - {game.Team2}, Goals:{game.Goals}");
        }
    }


    // Запит 9
    static void Query9(List<FootballGame> games)
    {
        //Query 9: Перетворити всі матчі UEFA Nations League у 2023 році на матчі з наступними властивостями:
        // MatchYear - рік матчу, Game - назви обох команд через дефіс (першою - Home_team), Result - результат для першої команди (Win, Loss, Draw)

        var selectedGames = games.Where(g=>g.Tournament== "UEFA Nations League"&&g.Date.Year==2023)
            .Select(g=>new
            {
                MatchYear=g.Date .Year ,
                Game=$"{g.Home_team}-{g.Away_team}",
                Result=g.Home_score>g.Away_score ?"Win":
                g.Home_score <g.Away_score ?"Loss":"Draw"
            });   // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 9 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.MatchYear} {game.Game}, Result for team1: {game.Result}");
        }
    }

    // Запит 10
    static void Query10(List<FootballGame> games)
    {
        //Query 10: Вивести з 5-го по 10-тий (включно) матчі Gold Cup, які відбулися у липні 2023 р.

        var selectedGames = games.Where(g=>g.Tournament== "Gold Cup"&&g.Date .Year==2023&&g.Date.Month==7)
            .OrderBy(g=>g.Date )
            .Skip(4)
           .Take(6);    // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 10 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }
}

```
**Код програми**

**FootballGame.cs**
```sh
public class FootballGame
 {
     public DateTime Date { get; set; }
     public string Home_team { get; set; }
     public string Away_team { get; set; }
     public int Home_score { get; set; }
     public int Away_score { get; set; }
     public string Tournament { get; set; }
     public string City { get; set; }
     public string Country { get; set; }
     public bool Neutral { get; set; }
 }
```
**Program.cs**
```sh
internal class Program
{
    static void Main(string[] args)
    {
        string path = @"../../../data/results_2010.json";

        List<FootballGame> games = ReadFromFileJson(path);

        int test_count = games.Count();
        Console.WriteLine($"Test value = {test_count}.");    // 13049

        Query1(games);
        Query2(games);
        Query3(games);
        Query4(games);
        Query5(games);
        Query6(games);
        Query7(games);
        Query8(games);
        Query9(games);
        Query10(games);
    }
    // Десеріалізація json-файлу у колекцію List<FootballGame>
    static List<FootballGame> ReadFromFileJson(string path)
    {
         var reader = new StreamReader(path);
        string jsondata = reader.ReadToEnd();
        List<FootballGame> games = JsonConvert.DeserializeObject<List<FootballGame>>(jsondata);
        return games;
    }
    // Запит 1
    static void Query1(List<FootballGame> games)
    {
        //Query 1: Вивести всі матчі, які відбулися в Україні у 2012 році.

        var selectedGames = games.Where(g=>g.Country=="Ukraine"&& g.Date.Year==2012); // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 1 ========================");
        foreach(var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }
    // Запит 2
    static void Query2(List<FootballGame> games)
    {
        //Query 2: Вивести Friendly матчі збірної Італії, які вона провела з 2020 року.  

        var selectedGames = games.Where(g=>g.Tournament=="Friendly"&&( g.Home_team=="Italy" || g.Away_team=="Italy")&& g.Date.Year >=2020); // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 2 ========================");
        foreach(var game in selectedGames )
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 3
    static void Query3(List<FootballGame> games)
    {
        //Query 3: Вивести всі домашні матчі збірної Франції за 2021 рік, де вона зіграла у нічию.

        var selectedGames = games.Where(g=>g.Country=="France"&& g.Date.Year ==2021 && g.Home_score==g.Away_score) ;   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 3 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 4
    static void Query4(List<FootballGame> games)
    {
        //Query 4: Вивести всі матчі збірної Германії з 2018 року по 2020 рік (включно), в яких вона на виїзді програла.

        var selectedGames = games.Where(g=>g.Away_team=="Germany"&&g.Date.Year>=2018 && g.Date.Year <=2020 && g.Away_score<g.Home_score);   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 4 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }
    // Запит 5
    static void Query5(List<FootballGame> games)
    {
        //Query 5: Вивести всі кваліфікаційні матчі (UEFA Euro qualification), які відбулися у Києві чи у Харкові, а також за умови перемоги української збірної.
        var selectedGames = games.Where(g => g.Tournament == "UEFA Euro qualification" && (g.City == "Kyiv" || g.City =="Kharkiv")&&g.Home_team=="Ukraine"&&g.Home_score>g.Away_score);  // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 5 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 6
    static void Query6(List<FootballGame> games)
    {
        //Query 6: Вивести всі матчі останнього чемпіоната світу з футболу (FIFA World Cup), починаючи з чвертьфіналів (тобто останні 8 матчів).
        //Матчі мають відображатися від фіналу до чвертьфіналів (тобто у зворотній послідовності).
        var selectedGames = games.Where(g=>g.Tournament == "FIFA World Cup"&&g.Date.Year==2022).OrderByDescending(g=>g.Date).Take(8);   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 6 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }

    // Запит 7
    static void Query7(List<FootballGame> games)
    {
        //Query 7: Вивести перший матч у 2023 році, в якому збірна України виграла.

        FootballGame g = games.Where(game => game.Date.Year == 2023 && 
        ((game.Home_team =="Ukraine"&& game.Home_score >game.Away_score) || 
        (game.Away_team == "Ukraine" && game.Away_score > game.Home_score)))
            .OrderBy(game=>game.Date)
            .FirstOrDefault();   // Корегуємо запит !!!
        // Перевірка
        Console.WriteLine("\n======================== QUERY 7 ========================");
        if(g!=null)
        {
            Console.WriteLine($"{g.Date:dd.MM.yyyy} {g.Home_team} - {g.Away_team}, Score: {g.Home_score} - {g.Away_score}, Country: {g.Country}");
        }
        else { Console.WriteLine("No matches found."); }
    }

    // Запит 8
    static void Query8(List<FootballGame> games)
    {
        //Query 8: Перетворити всі матчі Євро-2012 (UEFA Euro), які відбулися в Україні, на матчі з наступними властивостями:
        // MatchYear - рік матчу, Team1 - назва приймаючої команди, Team2 - назва гостьової команди, Goals - сума всіх голів за матч

        var selectedGames = games.Where(g => g.Tournament == "UEFA Euro" && g.Date.Year == 2012 && g.Country == "Ukraine")
            .Select(g => new
            {
                MatchYear = g.Date.Year,
                Team1=g.Home_team ,
                Team2=g.Away_team ,
                Goals=g.Home_score+g.Away_score
            });   // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 8 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.MatchYear} {game.Team1} - {game.Team2}, Goals:{game.Goals}");
        }
    }


    // Запит 9
    static void Query9(List<FootballGame> games)
    {
        //Query 9: Перетворити всі матчі UEFA Nations League у 2023 році на матчі з наступними властивостями:
        // MatchYear - рік матчу, Game - назви обох команд через дефіс (першою - Home_team), Result - результат для першої команди (Win, Loss, Draw)

        var selectedGames = games.Where(g=>g.Tournament== "UEFA Nations League"&&g.Date.Year==2023)
            .Select(g=>new
            {
                MatchYear=g.Date .Year ,
                Game=$"{g.Home_team}-{g.Away_team}",
                Result=g.Home_score>g.Away_score ?"Win":
                g.Home_score <g.Away_score ?"Loss":"Draw"
            });   // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 9 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.MatchYear} {game.Game}, Result for team1: {game.Result}");
        }
    }

    // Запит 10
    static void Query10(List<FootballGame> games)
    {
        //Query 10: Вивести з 5-го по 10-тий (включно) матчі Gold Cup, які відбулися у липні 2023 р.

        var selectedGames = games.Where(g=>g.Tournament== "Gold Cup"&&g.Date .Year==2023&&g.Date.Month==7)
            .OrderBy(g=>g.Date )
            .Skip(4)
           .Take(6);    // Корегуємо запит !!!

        // Перевірка
        Console.WriteLine("\n======================== QUERY 10 ========================");
        foreach (var game in selectedGames)
        {
            Console.WriteLine($"{game.Date:dd.MM.yyyy} {game.Home_team} - {game.Away_team}, Score: {game.Home_score} - {game.Away_score}, Country: {game.Country}");
        }
    }
}

```
**Результат роботи програми**

![Рисунок 1-результати тестування](https://github.com/Lia-st/Practice_Linq_2024_Velykorod/blob/master/1.png)

![Рисунок 2-результати тестування](https://github.com/Lia-st/Practice_Linq_2024_Velykorod/blob/master/2.png)

**Посилання на віддалений репозиторій**
https://github.com/Lia-st/Practice_Linq_2024_Velykorod.git
