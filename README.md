# Podstawowe konstrukcje jezyka ADA
Szablony podstawowych konstrukcji jezyka ADA, oraz szablony algorytmów synchronizacji.
## Spis tresci
### Podstawowe konstrukcje
1. [Tablice](#Tablice)
1. [Instrukcja warunkowa](#Instrukcja-warunkowa)
1. [Pętle](#pętle)
1. [Procedury](#Procedury)
1. [Funkcje](#Funkcje)
1. [Pakiety](#Pakiety)
1. [Zadania (task)](#zadania-task)

### Algorytmy synchronizacji
1. [Algorytm Petersona](#algorytm-petersona)

### Tablice
#### Deklaracja tablicy
```
_nazwa tablicy_ : array (1..n) of Typ;
```
```
tablica : array (1..10) of Integer;
```

#### Użycie tablicy - przypisanie
```
_nazwa tablicy_(index) := _wartosc_; 
```
```
tablica(10) := 10;
```

### Instrukcja warunkowa
```
if _wyrazenie logiczne_ then
  -- kod
  null;
elsif _wyrazenie logiczne_ then
  -- kod
  null;
else
  -- kod
  null;
end if;
```

### Pętle
#### for
```
for _zmienna_ in start..stop loop
  -- kod 
  null;
end loop;
```
#### while
```
while _wyrazenie logiczne_ loop
  -- kod
  null;
end loop;
```
#### loop
```
loop
  -- kod
  null;
  exit when _wyrazenie logiczne_;
end loop;
```

### Procedury
#### Deklaracje procedury
```
procedure _nazwa procedury_(parametr1,parametr2 : in/out Typ1; parametr3 : in/out Typ2);
```
#### Ciało procedury
```
procedure _nazwa procedury_(parametr1,parametr2 : Typ1; parametr3 : Typ2) is
-- miejsce na deklaracje zmiennych
begin
  -- kod
  null;
end _nazwa procedury_;
```

### Funkcje
#### Deklaracja funkcji
```
function _nazwa funkcji_(parametr : Typ1; parametr2,parametr3 : Typ2) return TypZwracany;
```
#### Ciało funkcji
```
function _nazwa funkcji_(parametr : Typ1; parametr2,parametr3 : Typ2) return TypZwracany is
-- miejsce na deklaracje zmiennych
begin
  -- kod
  null;
end _nazwa funkcji_;
```
### Pakiety
#### Plik \_nazwa pakietu\_.ads - deklaracja pakietu
```
package _nazwa pakietu_ is
  -- deklaracje funkcji i procedur
  -- function _nazwa funkcji_(parametr : Typ1; parametr2,parametr3 : Typ2) return TypZwracany;
  -- procedure _nazwa procedury_(parametr1,parametr2 : in/out Typ1; parametr3 : in/out Typ2);
end _nazwa pakietu_
```
#### Plik \_nazwa pakietu\_.adb - ciało pakietu
```
package body _nazwa pakietu_ is
  -- ciała funkcji i procedur
  -------------------------------------------------------------------------------------------
  function _nazwa funkcji_(parametr : Typ1; parametr2,parametr3 : Typ2) return TypZwracany is
  -- miejsce na deklaracje zmiennych
  begin
      -- kod
      null;
  end _nazwa funkcji_;
  --------------------------------------------------------------------------------------------
  procedure _nazwa procedury_(parametr1,parametr2 : Typ1; parametr3 : Typ2) is
  -- miejsce na deklaracje zmiennych
  begin
    -- kod
    null;
  end _nazwa procedury_;
  --------------------------------------------------------------------------------------------
end _nazwa pakietu_
```
### Zadania _task_
#### Deklaracja typu zadaniowego
```
task type _nazwa zadania_(parametr,parametr2 : Typ; parametr3 : Typ2);
```
#### Deklaracja ciała zadania
```
task body _nazwa zadania_ is
-- miejsce na deklaracje zmiennych zadania
begin
  -- kod
  null;
end _nazwa zadania_;
```

***
## Algorytmy Synchronizacji
### Algorytm Petersona
#### Dla dwóch różnych procesów
```
procedure Main is
   K1, K2 : Integer := 1;
   czyja_kolej : Integer := 1;
   
   procedure sekcjaLokalnaP1 is
      -- miejsce na deklaracje zmiennych
   begin
      -- kod
      null;
   end sekcjaLokalnaP1;
   
   procedure sekcjaLokalnaP2 is
      -- miejsce na deklaracje zmiennych
   begin
      -- kod
      null;
   end sekcjaLokalnaP2;
   
   procedure sekcjaKrytycznaP1 is
      -- miejsce na deklaracje zmiennych
   begin
      -- kod
      null;
   end sekcjaKrytycznaP1;
   
   procedure sekcjaKrytycznaP2 is
      -- miejsce na deklaracje zmiennych
   begin
      -- kod
      null;
   end sekcjaKrytycznaP2;
   
   
   task type P1(ile_razy : Integer);
   task type P2(ile_razy : Integer);
   
   task body P1 is
      -- zmienne
   begin
      for i in 1..ile_razy loop
         --------------------------------
         sekcjaLokalnaP1;
         --------------------------------
         K1 := 0;
         czyja_kolej := 2;
         while K2 = 0 and czyja_kolej = 2 loop
            null;
         end loop;
         --------------------------------
         sekcjaKrytycznaP1;
         --------------------------------
         K1 := 1;
      end loop;
   end P1;

   task body P2 is
      -- zmienne
   begin
      for i in 1..ile_razy loop
         --------------------------------
         sekcjaLokalnaP2;
         --------------------------------
         K2 := 0;
         czyja_kolej := 1;
         while K1 = 0 and czyja_kolej = 1 loop
            null;
         end loop;
         --------------------------------
         sekcjaKrytycznaP1;
         --------------------------------
         K2 := 1;
      end loop;
   end P2;


   taks1 : P1(10);
   task2 : P2(10);
begin
   --  Insert code here.
   null;
end Main;

```

---
&copy; Jakub Grątkiewicz
