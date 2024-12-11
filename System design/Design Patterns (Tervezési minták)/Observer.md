# Observer

Az Observer pattern egy viselkedési tervezési minta, amely egy olyan függőségi viszonyt definiál az objektumok között, ahol ha egy objektum (a Subject vagy Alany) állapota megváltozik, az összes függő objektum (Observer vagy Megfigyelő) automatikusan értesül és frissül. Ez a minta különösen hasznos eseményvezérelt rendszerekben és felhasználói felületek frissítésénél.

## Működése

1. **Subject (Alany)**: Ez az objektum tartalmazza az állapotot és kezeli a Megfigyelők listáját.

   - Metódusokat biztosít a Megfigyelők hozzáadására és eltávolítására.
   - Értesíti a Megfigyelőket az állapotváltozásról.

2. **Observer (Megfigyelő)**: Ez egy interfész vagy absztrakt osztály, amely definiálja az értesítési metódust.

3. **Concrete Observer (Konkrét Megfigyelő)**: Implementálja az Observer interfészt és frissíti magát, amikor értesítést kap.

### Példa PHP-ban:

```php
interface Subject {
    public function attach(Observer $observer);
    public function detach(Observer $observer);
    public function notify();
}

class ConcreteSubject implements Subject {
    private $observers = [];
    private $state;

    public function attach(Observer $observer) {
        $this->observers[] = $observer;
    }

    public function detach(Observer $observer) {
        $key = array_search($observer, $this->observers, true);
        if ($key !== false) {
            unset($this->observers[$key]);
        }
    }

    public function notify() {
        foreach ($this->observers as $observer) {
            $observer->update($this);
        }
    }

    public function setState($state) {
        $this->state = $state;
        $this->notify();
    }

    public function getState() {
        return $this->state;
    }
}

interface Observer {
    public function update(Subject $subject);
}

class ConcreteObserverA implements Observer {
    public function update(Subject $subject) {
        if ($subject->getState() < 3) {
            echo "ConcreteObserverA: Reagált az eseményre\n";
        }
    }
}

class ConcreteObserverB implements Observer {
    public function update(Subject $subject) {
        if ($subject->getState() >= 2) {
            echo "ConcreteObserverB: Reagált az eseményre\n";
        }
    }
}

// Használat
$subject = new ConcreteSubject();

$observerA = new ConcreteObserverA();
$observerB = new ConcreteObserverB();

$subject->attach($observerA);
$subject->attach($observerB);

$subject->setState(1);
$subject->setState(2);
$subject->setState(3);
```

## Előnyök

1. **Lazán csatolt objektumok**: A Subject nem ismeri a konkrét Observer osztályokat, csak az interfészt.
2. **Rugalmasság**: Könnyen hozzáadhatók és eltávolíthatók Observerek futásidőben.
3. **Broadcast kommunikáció**: Egy Subject egyszerre több Observert is értesíthet.

## Hátrányok

1. **Memóriahasználat**: Nagy számú Observer esetén jelentős lehet a memóriahasználat.
2. **Teljesítmény**: Sok Observer esetén az értesítések lelassíthatják a rendszert.
3. **Váratlan frissítések**: Az Observerek nem tudják, hogy más Observerek is frissülnek-e, ami váratlan eredményekhez vezethet.

Az Observer pattern különösen hasznos olyan helyzetekben, ahol egy objektum állapotváltozása több más objektum viselkedését befolyásolja, például grafikus felhasználói felületek eseménykezelésénél vagy adatbázis-változások követésénél.