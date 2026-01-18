
# Člověče, nezlob se 1D


1. Zjednodušené "Člověče, nezlob se" se hraje na hracím plánu velikosti **10** polí pouze s jednou figurkou. 

2. Figurka se posunuje podle hodů kostkou, tj. podle náhodné generovaných čísel 1 - 6. Pokud padne číslo 6, **házíme znova** a čísla sčítáme. Figurka se posunuje o **celkový součet**.

3. Hra končí, jakmile dorazíme na poslední pole, přičemž se musíme trefit **přesně** na poslední pole. Pokud se netrefíme, figurka stojí (číslo bude **čevené**). Program hozená čísla v řadě za sebou vypíše.

4. Na dalším řádku pak **počet** spotřebovaných tahů figurkou.

5. Pokud se to podaří bez "čekacích hodů", vypíše se **gratulace**.

🎲 Živá ukázka: [https://php.edumach.cz/clovece_1d.php](https://php.edumach.cz/clovece_1d.php)


## Použité PHP konstrukce

1. Generátor náhodných čísel `rand(1,6)` - hod kostkou.
2. Cyklus řízený podmínkou `while` - hlavní smyčka programu. Běží dokud figurka nedorazí na poslední pole.
3. Vlastní funkce `function hod()` s návratovou hodnotou `return $soucet` - generuje hod kostkou včetně opakovaných hodů, pokud padne 6. Součet pak vrátí do hlavní smyčky. 
4. Cyklus řízený podmínkou `do-while` - generuje hod kostkou uvnitř funkce `hod()`.
5. Úplné větvení `if-else` - testuje a řídí stavy hry:
   - Lze ještě tánnout figurkou? `$hod <= $zbyva`. V Opačném případě figurka stojí (červeně).
   - Dohráno bez čekacích hodů (zeleně)? `$cekani == False`
6. "Vlajka" (flag), která drží informaci, zda došlo k čekacímu hodu. Na začátku je nastavena na `$cekani = False`. Pokud figurka čeká, nastaví se na `True`.


### Funkce pro hod kostkou

```php
// funkce pro hod kostkou
function hod_kostkou()
  {
    $soucet = 0; // inicializace součtu bodů
    do
    {
      $hod = rand(1, 6); // hoď kostkou
      $soucet += $hod; // přičti k předchozím bodům 
    } while ($hod == 6); // opakuj hod, pokud padla 6

    return $soucet; // vrať celkový součet 
  }
```  

### Inicializace proměnných

Pod funkcí inicializujeme pracovní proměnné:

```php
$n = 10; // délka hracího plánu
$zbyva = $n; // kolik ještě figurce zbývá (její pozice) 
$pocet_tahu = 0; // počet tahů pro celkovou statistiku
$cekani = False;  // čekací hod

// Inicializace výpisu hodů. 
// Konec odstavce </p> bude až figurka dosálne cíle.
echo "<p>Hody: "; 
```

### Hlavní smyčka programu

Tělo smyčky se bude opakovat, dokud figurka nedosáhla cílového pole. 

```php
while ($zbyva > 0)
{
    // hlavní smyčka programu
}
```

Co bude smyčka obsahovat?

1. Hod kostkou a inkrementace počítadla hodů:
    ```php
    $hod = hod_kostkou(); // hoď kostkou 
    $pocet_tahu++; // zvyš počítadlo tahů o 1
    ``` 
2. Podmínku, která rozhodne, zda se může figurka posunout (proměnná `$hod` je menší nebo rovná `$zbyva`):
    - Pokud ano (podmínka vrátí `True`):
        ```php
        echo $hod . " "; // vypiš hod a přidej mezeru
        $zbyva -= $hod; // "posuň" figurku 
        ``` 
    - Pokud ne (podmínka vrátí `False`):   
        ```php
        // vypiš hod červeně
        echo "<span style='color:red;'>" . $hod . "</span>";
        // nastav $cekani na True   
        $cekani = True;
        ```
        Co je značka `<span>`: [https://www.w3schools.com/tags/tag_span.asp](https://www.w3schools.com/tags/tag_span.asp)

### Výpis statistiky a gratulace (SAMOSTATNĚ DOPIŠTE)
1. Pod tělem smyčky `while` se musí nejprve ukončit odstavec, kam se vypisovaly hody: `echo "</p>";`.
2. **Odstavec**, který vypíše počet spotřebovaných tahů.
3. Pokud nebyl ani jeden čekací hod, vypiš **odstavec** s gratulací zeleně.


## Odevzdání
- Funkční skript podle zadání na dané URL. Kontrolu si provedu přímo tam.

