A Strategy (Stratégia) pattern egy viselkedési tervezési minta, amely lehetővé teszi algoritmusok dinamikus cseréjét futásidőben. Ez a minta különösen hasznos, amikor különböző variációi vannak egy algoritmusnak, és ezeket rugalmasan szeretnénk cserélni anélkül, hogy módosítanánk a kliens kódot.

## Hogyan működik?

1. **Strategy (Stratégia) interfész**: Definiálja az algoritmus közös interfészét.

2. **Concrete Strategies (Konkrét Stratégiák)**: Implementálják a Strategy interfészt, megvalósítva a specifikus algoritmusokat.

3. **Context (Kontextus)**: Tartalmaz egy referenciát egy Strategy objektumra, és használja azt a műveletek végrehajtására.

## Példa PHP-ban:

```php
// Strategy interfész
interface SortStrategy {
    public function sort(array $data): array;
}

// Konkrét Stratégiák
class BubbleSort implements SortStrategy {
    public function sort(array $data): array {
        echo "Buborékrendezés alkalmazása\n";
        // Buborékrendezés implementációja
        return $data;
    }
}

class QuickSort implements SortStrategy {
    public function sort(array $data): array {
        echo "Gyorsrendezés alkalmazása\n";
        // Gyorsrendezés implementációja
        return $data;
    }
}

// Context
class Sorter {
    private $sortStrategy;

    public function __construct(SortStrategy $sortStrategy) {
        $this->sortStrategy = $sortStrategy;
    }

    public function setSortStrategy(SortStrategy $sortStrategy) {
        $this->sortStrategy = $sortStrategy;
    }

    public function sort(array $data): array {
        return $this->sortStrategy->sort($data);
    }
}

// Használat
$data = [5, 2, 8, 12, 1, 6];

$sorter = new Sorter(new BubbleSort());
$sorter->sort($data);

$sorter->setSortStrategy(new QuickSort());
$sorter->sort($data);
```

## Előnyök:

1. **Rugalmasság**: Könnyen cserélhető algoritmusok futásidőben.
2. **Nyílt/zárt elv**: Új stratégiák adhatók hozzá anélkül, hogy módosítanánk a meglévő kódot.
3. **Elkülönítés**: Az algoritmusok elkülönülnek a kliens kódtól.
4. **Alternatívák**: Több alternatív megoldást kínál egy probléma megoldására.

## Hátrányok:

1. **Komplexitás**: Növelheti a kód komplexitását, ha csak néhány algoritmus van.
2. **Kontextus ismerete**: A kliensnek ismernie kell a különböző stratégiákat.
3. **Kommunikációs overhead**: A stratégia és a kontextus közötti kommunikáció növelheti az overhead-et.

A Strategy pattern különösen hasznos olyan helyzetekben, ahol több algoritmus vagy viselkedés közül kell választani futásidőben, például különböző fizetési módok kezelésénél egy webshopban, vagy különböző útvonaltervezési algoritmusok alkalmazásánál egy navigációs rendszerben.