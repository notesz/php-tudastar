# A CQRS gyakorlati alkalmazása

A CQRS (Command Query Responsibility Segregation) gyakorlati megvalósítása a következőképpen működik:

## Alapvető struktúra

A CQRS két fő komponensre osztja a rendszert:

1. **Parancsok (Commands)**: Az adatok módosítására szolgálnak.
2. **Lekérdezések (Queries)**: Az adatok lekérésére szolgálnak.

## Parancsok megvalósítása

A parancsok kezelése általában a következő lépésekből áll:

1. Parancs objektum létrehozása
2. Parancs kezelő (handler) implementálása
3. Parancs végrehajtása

Példa egy parancs objektumra:

```php
class CreateProductCommand implements Command
{
    public function __construct(
        private string $name,
        private float $price
    ) {}

    public function getName(): string
    {
        return $this->name;
    }

    public function getPrice(): float
    {
        return $this->price;
    }
}
```

Példa egy parancs kezelőre:

```php
class CreateProductCommandHandler implements CommandHandler
{
    public function __construct(private ProductRepository $repository)
    {}

    public function handle(CreateProductCommand $command): void
    {
        $product = new Product($command->getName(), $command->getPrice());
        $this->repository->save($product);
    }
}
```

## Lekérdezések megvalósítása

A lekérdezések hasonló struktúrát követnek:

1. Lekérdezés objektum létrehozása
2. Lekérdezés kezelő implementálása
3. Lekérdezés végrehajtása

Példa egy lekérdezés objektumra:

```php
class ProductSimpleQuery
{
    public function __construct(private int $productId)
    {}

    public function getProductId(): int
    {
        return $this->productId;
    }
}
```

Példa egy lekérdezés kezelőre:

```php
class ProductSimpleQueryHandler
{
    public function __construct(private ProductRepository $repository)
    {}

    public function handle(ProductSimpleQuery $query): array
    {
        $product = $this->repository->findById($query->getProductId());
        return [
            'name' => $product->getName(),
            'price' => $product->getPrice(),
        ];
    }
}
```

## Használat a gyakorlatban

A CQRS használata egy kontroller osztályban:

```php
class ProductController extends Controller
{
    public function __construct(
        private CommandBus $commandBus,
        private QueryBus $queryBus
    ) {}

    public function create(Request $request)
    {
        $command = new CreateProductCommand(
            $request->input('name'),
            $request->input('price')
        );
        $this->commandBus->dispatch($command);
    }

    public function details(int $id)
    {
        $query = new ProductSimpleQuery($id);
        return $this->queryBus->ask($query);
    }
}
```

## Előnyök

1. Jobb teljesítmény és skálázhatóság
2. Egyszerűbb kód és karbantarthatóság
3. Rugalmasabb rendszertervezés

A CQRS PHP-ban történő megvalósítása lehetővé teszi a fejlesztők számára, hogy elkülönítsék az adatmódosítási és lekérdezési műveleteket, ami javítja a kód szervezettségét és a rendszer teljesítményét.