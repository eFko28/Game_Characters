# Game_Characters_OOP

Vytvořte systém herních postav, který demonstruje základy a pokročilé principy OOP.
Postavy budou mít atributy, schopnosti a možnost interakce. Budou existovat různé typy postav
využívající dědičnost, dundery a dekorátory.

---

# STEP 01

## Funkcionalita
1. Třída `Character` definuje základní vlastnosti a metody postav.
2. Dědičné třídy `Warrior` a `Mage` mají specifické schopnosti.
3. Použití dunder metod pro interakci s objekty (např. stringová reprezentace, kombinace inventáře).
4. Použití dekorátorů pro přidání speciálních efektů (např. zvýšení síly).

## Postup
1. **Definice základní třídy `Character`**:
    - Atributy: `name`, `health`, `mana`, `level`.
    - Metody: `__init__`, `__str__`, `defend`, `__add__`.

2. **Definice třídy `Warrior`**:
    - Dědí z `Character`.
    - Atributy: `attack_power`, `defense`.
    - Metody: `__init__`, `attack`.

3. **Definice třídy `Mage`**:
    - Dědí z `Character`.
    - Atributy: `intelligence`.
    - Metody: `__init__`, `cast_spell`.

4. **Použití dekorátoru `power_boost`**:
    - Definice dekorátoru, který zvýší sílu útoku.
    - Použití dekorátoru na metodu `attack` třídy `Warrior`.

5. **Ukázka použití**:
    - Vytvoření instancí `Warrior` a `Mage`.
    - Demonstrace základních operací: útok, obrana, kombinace inventářů.

```python
##############################################################
def power_boost(func):
    """Dekorátor, který zvýší sílu útoku.
    Dekorátor přidá pevnou hodnotu 10 k základnímu poškození vrácenému původní funkcí.
    Také vytiskne zprávu, že síla útoku byla zvýšena. Využití u válečníka.
    Args:
        func: Původní funkce, která vrací základní poškození.
    Returns:
        wrapper: Nová funkce, která vrací zvýšené poškození a vypíše info.
     """

    def wrapper(*args, **kwargs):
        """Upravená funkce s přidaným efektem. Načte základní poškození a přidá 10 bodů."""
        base_damage = func(*args, **kwargs)
        boosted_damage = base_damage + 10
        print("Síla útoku byla zvýšena o 10 bodů!")
        return boosted_damage

    return wrapper

##############################################################
class Character:
    """Základní třída pro všechny herní postavy.
    Args:
        name (str): Jméno postavy.
        health (int): Zdraví postavy.
        mana (int): Mana postavy.
        level (int): Úroveň postavy.
    Methods:
        defend: Obrana postavy proti útoku.
    Attributes:
        __str__: Textová reprezentace postavy - dunder.
        __add__: Kombinace inventářů dvou postav - dunder.
    """
...

    def __add__(self, other):
        """Kombinace inventářů dvou postav (dunder pro sčítání)."""
        if isinstance(other, Character):
            combined_inventory = self.inventory + other.inventory
            return combined_inventory
        raise ValueError("Lze kombinovat pouze inventáře postav.")

##############################################################
class Warrior(Character):
    """Válečník je podtřída třídy Character, která představuje válečníka ve hře,
    specializovaného na fyzické útoky.
    Attributes:
        name (str): Jméno válečníka.
        health (int): Zdraví válečníka.
        mana (int): Mana válečníka.
        level (int): Úroveň válečníka, která ovlivňuje jeho sílu.
        strength (int): Fyzická síla válečníka, vypočítaná jako level * 5.
    Methods:
        __init__(name: str, health: int, mana: int, level: int):
            Inicializuje nového válečníka se zadaným jménem, zdravím, manou a úrovní.
        attack():
            Provádí silný fyzický útok. Způsobené poškození je součtem základního
            poškození útoku z třídy Character a síly válečníka.
    """

##############################################################
class Mage(Character):
    """Třída Mage reprezentuje kouzelníka, který je specializovaný na magické útoky.
    Attributes:
        name (str): Jméno kouzelníka.
        health (int): Zdraví kouzelníka.
        mana (int): Mana kouzelníka, potřebná pro kouzlení.
        level (int): Úroveň kouzelníka, která ovlivňuje jeho schopnosti.
        intelligence (int): Inteligence kouzelníka, závislá na jeho úrovni.
    Methods:
        cast_spell(): 
            Seslání kouzla, které spotřebuje manu a způsobí náhodné 
            poškození v závislosti na úrovni kouzelníka.
    """

##############################################################
if __name__ == "__main__":
    os.system('clear' if os.name == 'posix' else 'cls')

    # Vytvoření postav
    hero1 = Warrior("Válek", 100, 20, 5)
    hero2 = Mage("Hrnčiřík", 80, 50, 4)

    # Základní operace
    print(hero1)
    print(hero2)
    print ("-"*40)

    # Útok a obrana
    damage = hero1.attack()
    print(f"{hero1.name} útočí a způsobuje {damage} poškození.")
    hero2.defend(damage)
    print(f"Po útoku má {hero2.name} {hero2.health} zdraví.")
    print ("-"*40)

    # Kombinace inventářů
    hero1.inventory.append("Meč")
    hero1.inventory.append("Kožená vesta")
    hero2.inventory.append("Hůl")
    print(f"Inventář {hero1.name}: {hero1.inventory}")
    print(f"Inventář {hero2.name}: {hero2.inventory}")
    print ("-"*40)
    
    combined_inventory = hero1 + hero2
    print(f"Kombinovaný inventář: {combined_inventory}")

    print ("-"*40)
    print(f"Inventář {hero1.name}: {hero1.inventory}")
    print(f"Inventář {hero2.name}: {hero2.inventory}")
    print ("-"*40)
    hero1.inventory = hero1 + hero2
    print (f"Do inventáře {hero1.name} byl přidán inventář {hero2.name}.")
    print(f"Inventář {hero1.name}: {hero1.inventory}")
    print(f"Inventář {hero2.name}: {hero2.inventory}")
    print ("-"*40)
##############################################################
```

**Terminál:**
```sh
Válek (Úroveň: 5, Zdraví: 100, Mana: 20, Inventář: [])  
Hrnčiřík (Úroveň: 4, Zdraví: 80, Mana: 50, Inventář: [])
----------------------------------------
Síla útoku byla zvýšena o 10 bodů!
Válek útočí a způsobuje 45 poškození.
Po útoku má Hrnčiřík 39 zdraví.
----------------------------------------
Inventář Válek: ['Meč', 'Kožená vesta']
Inventář Hrnčiřík: ['Hůl']
----------------------------------------
Kombinovaný inventář: ['Meč', 'Kožená vesta', 'Hůl']    
----------------------------------------
Inventář Válek: ['Meč', 'Kožená vesta']
Inventář Hrnčiřík: ['Hůl']
----------------------------------------
Do inventáře Válek byl přidán inventář Hrnčiřík.        
Inventář Válek: ['Meč', 'Kožená vesta', 'Hůl']
Inventář Hrnčiřík: ['Hůl']
```

---

# STEP 02

Rozšíření systému herních postav o abstraktní třídu, vlastnosti a další OOP principy.

## Nové funkcionality
1. Přidání abstraktní třídy `PlayableCharacter`, která definuje základní rozhraní pro 
    všechny hratelné postavy. Tato třída obsahuje abstraktní metody, které musí být 
    implementovány ve všech potomcích.
2. Implementace vlastností pomocí dekorátoru `@property` pro kontrolu atributů, 
    jako je například maximální zdraví postavy. Vlastnosti umožňují kontrolovat a validovat 
    hodnoty atributů při jejich nastavování.
3. Rozšíření třídy `Character` o metody využívající vlastnosti a abstraktní metody. 
    Třída `Character` slouží jako základní třída pro všechny herní postavy a implementuje 
    základní funkce jako útok, obrana a zvýšení úrovně.
Specializované třídy `Warrior` a `Mage`, které dědí z třídy `Character` a přidávají specifické 
vlastnosti a metody pro válečníka a kouzelníka. Třída `Warrior` je zaměřena na fyzické útoky a má 
speciální bonusy k síle, zatímco třída `Mage` je zaměřena na magické útoky a má bonusy k inteligenci.

## Funkce útoku a obrany
- Funkce útoku v základní třídě `Character` počítá základní poškození útoku tak, že vygeneruje náhodné celé číslo mezi 1 a 10 a vynásobí ho úrovní postavy.
- Funkce obrany snižuje zdraví postavy o přijaté poškození snížené o úroveň postavy, dále řeší, aby se zabránilo záporným hodnotám zdraví.
- Třída `Warrior` přepisuje funkci útoku tak, aby zahrnovala bonus k síle, který se počítá jako úroveň postavy vynásobená 5. 
- Dekorátor `power_boost` dále zvyšuje poškození útoku o pevnou hodnotu 10.
- Třída `Mage` zavádí funkci `cast_spell`, která spotřebovává manu o 10 k provedení magického útoku, přičemž poškození je založeno na úrovni postavy a náhodném faktoru.
- Obě třídy mají metodu `level_up`, která zvyšuje úroveň postavy a přidává bonusy k síle nebo inteligenci.

```python
##############################################################
# Abstraktní třída PlayableCharacter
# Základní rozhraní pro všechny hratelné postavy
# Musí být implementována ve všech potomcích
# Metody: attack, defend, level_up

class PlayableCharacter(ABC):
    """Abstraktní třída definující základní rozhraní pro všechny hratelné postavy."""

    @abstractmethod
...

##############################################################
...
    @health.setter
    def health(self, value):
        """Nastavení zdraví s kontrolou nula až max."""
        if value > self.MAX_HEALTH:
            self._health = self.MAX_HEALTH
        elif value < 0:
            self._health = 0  # Zdraví nesmí být záporné
        else:
            self._health = value
...

```

---

# STEP 03
Rozšíření/úprava systému herních postav o demonstraci `Public`, `Protected` a `Private` atributů.

## Teorie
- Public atributy/metody:
    - Jsou volně přístupné odkudkoliv (zvenčí i zevnitř třídy).
    - Žádná speciální syntaxe, např. `self.name`.
- Protected atributy/metody:
    - Označují se jedním podtržítkem _ (např. `self._health`).
    - Označuje, že by atribut/metoda neměla být přístupná přímo mimo třídu nebo její potomky, ale není striktně omezen.
    - Používá se ke sdílení mezi třídou a jejími podtřídami.
    - Ošetření pomocí setter property (viz výše).
- Private atributy/metody:
    - Označují se dvěma podtržítky __ (např. `self.__mana`).
    - Python je interně přejmenuje (name mangling), což zabrání přímému přístupu zvenčí třídy.

```python
##############################################################
...
    def _use_mana(self, amount: int):
        """Protected metoda: Použití many. Určeno pro interní použití nebo potomky."""
        if self.__mana >= amount:
            self.__mana -= amount
            return True
        return False
...

```
---

# STEP 04

Přidáme do hlavní části programu náhodný průběh hry, kde postavy bojují proti sobě. 

## Implementujeme
- Generování náhodných postav na začátku hry.
- Náhodný střet postav v nekonečném cyklu.

## Simulace boje
- Každá postava provede útok nebo obranu.
- Zobrazení průběhu boje v terminálu s krátkými prodlevami (`time.sleep()`).
- Konec hry: Pokud některá postava dosáhne 0 zdraví, hra skončí a zobrazí vítěze.

```python
##############################################################
def generate_random_character() -> Character:
    """Vygeneruje náhodnou herní postavu."""

##############################################################
def battle_round(character1: Character, character2: Character):
    """Simuluje jedno kolo boje mezi dvěma postavami."""

##############################################################
# Funkce pro simulaci průběhu hry

def game_loop():
    """Hlavní herní smyčka."""
    print("=== Začíná hra ===\n")
    time.sleep(1)

    # Generujeme dvě náhodné postavy
    player1 = generate_random_character()
    player2 = generate_random_character()

    print("Vygenerované postavy:")
    print(player1)
    print(player2)

    # Hlavní smyčka
    while True:
        winner = battle_round(player1, player2)
        if winner:
            print(f"\n=== Hra skončila! Vítězem je {winner.name} ===")
            break
        time.sleep(2)
```

---

# STEP 05

## Generování 3–5 postav
- Vytvoříme více herních postav, které budou hrát hru.
- Postavy budou uloženy v seznamu.

## Náhodné souboje
- Pro každé kolo náhodně vybereme dva různé hráče, kteří budou bojovat.

## Zobrazení stavu po každém kole
- Po každém kole zobrazíme aktuální stav všech postav.

## Náhodné události
- Implementujeme události, které mohou náhodně ovlivnit postavy mezi koly, například:
        - Uzdravení postavy.
        - Získání nového předmětu.
        - Ztráta části zdraví.

```python
##############################################################
def generate_random_characters(num: int) -> list:
    """Vygeneruje seznam náhodných herních postav.
    Args:
        num (int): Počet postav k vygenerování.
    Returns:
        list: Seznam postav.
    """

##############################################################
def display_characters_status(characters: list):
    """Zobrazí aktuální stav všech postav.
    Args:
        characters (list): Seznam postav.
    """

##############################################################
def random_event(characters: list):
    """Provede náhodné události mezi koly.
    Args:
        characters (list): Seznam postav.
    """
```

**Výstup v terminálu:**

```sh
=== Začíná hra ===

Vygenerované postavy:
Thor (Úroveň: 3, Zdraví: 150, Mana: 20, Inventář: prázdný)
Merlin (Úroveň: 5, Zdraví: 100, Mana: 50, Inventář: prázdný)
Conan (Úroveň: 4, Zdraví: 180, Mana: 30, Inventář: prázdný)

=== Nové kolo ===
Thor a Merlin se utkají v boji!

--- Kolo boje ---
Thor útočí a způsobuje 18 poškození.
Merlin má nyní 82 zdraví.
Merlin útočí a způsobuje 42 poškození.
Thor má nyní 108 zdraví.

=== Aktuální stav postav ===
Thor (Úroveň: 3, Zdraví: 108, Mana: 20, Inventář: prázdný)
Merlin (Úroveň: 5, Zdraví: 82, Mana: 40, Inventář: prázdný)
Conan (Úroveň: 4, Zdraví: 180, Mana: 30, Inventář: prázdný)

=== Náhodné události ===
Merlin ztrácí 15 zdraví.
Conan získal nový předmět: Magic Scroll.
...
=== Hra skončila! Vítězem je Conan ===
```
---

# STEP 06
Přidáme mechaniku náhodného setkání s příšerou, což dá hře další rozměr. Každá postava může náhodně potkat příšeru 
a bojovat s ní během hry. Příšery budou mít své atributy, jako je zdraví, síla a náhodná šance na speciální útok.

## Třída Monster
- Reprezentuje příšeru s atributy a jednoduchým chováním.
- Příšery budou generovány náhodně s různou sílou a zdravím.
- Reprezentuje příšery s atributy `health` (zdraví) a `strength` (síla útoku).
- Obsahuje metody `attack()` a `defend()` pro boj.

## Mechanika setkání
- Náhodně vybereme postavu, která potká příšeru.
- Simulujeme boj mezi postavou a příšerou.
- Pokud postava porazí příšeru, může získat odměnu (např. zdraví nebo předmět).
- `monster_encounter()`:
        - Simuluje boj mezi postavou a příšerou.
        - Pokud postava porazí příšeru, získá odměnu: uzdravení nebo nový předmět.

## Změny v herní smyčce (`game_loop`)
- Přidána náhodná šance (30 %) na setkání s příšerou před každým kolem boje.

```python
##############################################################
class Monster:
    """Třída reprezentující příšeru."""

##############################################################
def generate_random_monster() -> Monster:
    """Vytvoří náhodnou příšeru."""

##############################################################
def monster_encounter(character: Character):
    """Simuluje setkání postavy s příšerou."""
    monster = generate_random_monster()
    print(f"\n{character.name} narazil na {monster}!")
    time.sleep(1)
...
```

**Terminál:**

```sh
=== Začíná hra ===

Vygenerované postavy:
Thor (Úroveň: 3, Zdraví: 150, Mana: 20, Inventář: prázdný)
Merlin (Úroveň: 5, Zdraví: 100, Mana: 50, Inventář: prázdný)
Conan (Úroveň: 4, Zdraví: 180, Mana: 30, Inventář: prázdný)

=== Nové kolo ===
Merlin narazil na Příšera Goblin (Zdraví: 70, Síla: 15)!

Merlin útočí a způsobuje 25 poškození.
Goblin má nyní 45 zdraví.
Goblin útočí a způsobuje 10 poškození.
Merlin má nyní 90 zdraví.

Merlin útočí a způsobuje 30 poškození.
Goblin byl poražen!
Merlin získává 35 zdraví jako odměnu.

...

=== Hra skončila! Vítězem je Conan ===
```

