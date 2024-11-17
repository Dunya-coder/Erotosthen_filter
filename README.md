# Erotosthen_filter
``` Cs
using System;
using System.IO;

class Goldbach
{
    // Eratosthen filtri orqali tub sonlarni aniqlash
    static bool[] SieveOfEratosthenes(int limit)
    {
        bool[] primes = new bool[limit + 1];
        for (int i = 0; i <= limit; i++) primes[i] = true;
        primes[0] = primes[1] = false;

        for (int i = 2; i * i <= limit; i++)
        {
            if (primes[i])
            {
                for (int j = i * i; j <= limit; j += i)
                {
                    primes[j] = false;
                }
            }
        }

        return primes;
    }

    // Goldbax juftligini topish
    static (int, int) FindGoldbachPair(int n, bool[] primes)
    {
        for (int i = 2; i <= n / 2; i++)
        {
            if (primes[i] && primes[n - i])
            {
                return (i, n - i);
            }
        }

        return (0, 0);
    }

    static void Main(string[] args)
    {
        // INPUT.TXT faylidan sonni o‘qish
        int n = int.Parse(File.ReadAllText("INPUT.TXT").Trim());

        // Eratosthen filtrini ishlatish
        bool[] primes = SieveOfEratosthenes(n);

        // Goldbax juftligini topish
        var (a, b) = FindGoldbachPair(n, primes);

        // OUTPUT.TXT fayliga natijani yozish
        File.WriteAllText("OUTPUT.TXT", $"{a} {b}\n");
    }
}
```
Kod qanday ishlaydi:
isPrime massiv: Barcha sonlar avval true deb belgilanadi (tub deb qabul qilinadi).
Filtrlash: 2 dan boshlanadi, har bir tub son uchun uning ko‘paytmalari false deb belgilanadi (tub emas).
Natija: Tub sonlar ro‘yxatga qo‘shiladi va konsolga chiqariladi.
Vaqt murakkabligi: 
𝑂
(
𝑁
log
⁡
log
⁡
𝑁
)
O(NloglogN) — Eratosthen filtri juda samarali algoritmdir.
Xotira murakkabligi: 
𝑂
(
𝑁
)
O(N) — Bu algoritm isPrime massiviga ega bo‘lgani uchun.
