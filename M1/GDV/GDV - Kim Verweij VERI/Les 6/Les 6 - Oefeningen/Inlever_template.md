# Mini-level — Inleveren

Naam: Thijmen van der Zwan
Klas: SD1A
Datum: 11-11-2026
Les: GDV Les 6

Ik heb een mini-game gemaakt waarin je kogels moet blokkeren met een schild. Elke kogel die je schild raakt geeft 1 punt, elke kogel die je karakter raakt doet 20 damage. Je hebt 100 hp, en moet zoveel mogelijk punten behalen voordat je dood gaat.

<img width="722" height="664" alt="MiniLevel" src="https://github.com/user-attachments/assets/dfb72f63-902d-41d9-a7a7-d4a493874bb4" />

## Bewegend object
De code maakt eerst een variable aan die naar het punt voor de kogel gaat, waardoor de kogel altijd vooruit gaat, zodat ik de code niet hoef aan te passen op alle 4 de richtingen.

...

```csharp
Vector3 dir = transform.forward;
dir = transform.InverseTransformDirection(dir);
dir.y = 0;
dir.Normalize();

transform.position += 1 * Time.deltaTime * transform.right * mod;
```

---

## Collider of trigger

Als de kogel het doelwit of het schild raakt, gaat hij stuk.

...

```csharp
private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("shield"))
    {
        Destroy(gameObject);
    }
    if (other.CompareTag("target"))
    {
        Destroy(gameObject);
    }
}
```
Als de speler wordt geraakt door een kogel, verliest hij 20hp, en verschijnt dat direct in de hoek als tekst, maar als je schild ham raakt wordt je beloond!

...

```csharp
private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("bullet"))
    {
        Hitpoints -= 20;
        txt.text = "HP: " + Hitpoints.ToString();
    }
}

private void OnTriggerEnter(Collider other)
{
    if (other.CompareTag("bullet"))
    {
        points += 1;
        txt.text = "Points: " + points.ToString();
    }
}
```

---

## Logica met `if` of `switch`

Deze haalt een willekeurige waarde op, pakt dan de coordinaten uit een array en draait de kogel in een bepaalde richting. Ik had de richting ook in een array kunnen zetten, maar ik was daar te onzeker van ivm richting.

...

```csharp
int spawn = Random.Range(0, 4);
switch (spawn)
{
    case 0:
        Instantiate(bullet, spawnpos[spawn], Quaternion.Euler(0, 270, 0));
        break;
    case 1:
        Instantiate(bullet, spawnpos[spawn], Quaternion.Euler(0, 90, 0));
        break;
    case 2:
        Instantiate(bullet, spawnpos[spawn], Quaternion.Euler(0, 180, 0));
        break;
    case 3:
        Instantiate(bullet, spawnpos[spawn], Quaternion.Euler(0, 0, 0));
        break;

}
```
Deze haalt input op, en roept dan de functie RotPlayer(axis) om aan te roepen dat de speler met het schild draait

...

```csharp
if (Input.GetKey(upKey))
{
    RotPlayer(0f);
}
else if (Input.GetKey(rightKey))
{
    RotPlayer(90f);
}
else if (Input.GetKey(downKey))
{
    RotPlayer(180f);
}
else if (Input.GetKey(leftKey))
{
    RotPlayer(270f);
}
```

---

## Eigen extra idee

Ik heb zelf willekeurige waarde toegevoegd, zodat het spel onvoorspelbaar blijft. Dit heb ik eerder al benoemd.



## Evaluatie

Ik ben heel blij met hoe dit projectje is gelukt. Ik had een idee in mijn hoofd wat redelijk te doen zou zijn, en het is gewoon 1 op 1 wat ik ervan verwacht had, en het is ook best leuk om te spelen. Ik had nog wel moeite met de logica achter het willekeurig instantiaten van de kogels, tot een punt waar ik mijn Windows ermee heb gecrasht, omdat hij heel vaak achter elkaar op 4 verschillende punten elke frame 4 kogels genereerde. Volgende keer ga ik daarom zorgen dat mijn if statements werken voordat ik ze klakkeloos uitvoer. 

...
