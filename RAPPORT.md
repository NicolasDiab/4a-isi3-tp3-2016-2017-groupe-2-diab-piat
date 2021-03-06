**Nom/Prénom Etudiant 1 :** DIAB Nicolas

**Nom/Prénom Etudiant 2 :** PIAT Grégoire

# Rapport TP3

## Question 1
Nous allons tester si les méthodes getAge et wasBorn dans les cas suivants :
- Au début d'année de sa naissance
- A la fin d'année de sa naissance
- 10 ans avant sa naissance
- 10 ans après sa naissance

@TODO ajouter les classes d'équivalence


## Question 2

Tous les tests de la classe PersonTest passent sans erreur.

## Question 3

Voir PeopleTest.

## Question 4

Chacune des classes possède un test qui ne passe pas.

## Question 5
Pattern adapter (PersonneAdapter)

## Question 6

Dans la classe OutilsPerson :
```java
public static List<IPerson> getPersonsOnRange(List<IPerson> persons, GregorianCalendar date, int minAge, int maxAge) throws IllegalArgumentException{

    if (minAge > maxAge)
        throw new IllegalArgumentException();

    List<IPerson> personsOnRange = new ArrayList<>();

    if (persons.size() == 0)
        return new ArrayList<>();

    for (IPerson person : persons){
        if (person.getAge(date) >= minAge && person.getAge(date) <= maxAge)
            personsOnRange.add(person);
    }

    return personsOnRange;
}
```

## Question 7

Dans la classe OutilsPerson :
```java
public static int getMaxAge(List<IPerson> persons, GregorianCalendar date){

    int maxAge = -1;

    if (persons.size() == 0)
        return -1;

    for (IPerson person : persons){
        if (person.getAge(date) > maxAge)
            maxAge = person.getAge(date);
    }

    return maxAge;
}
```

## Question 8

Les tests des fonctions getMaxAge() et getPersonsOnRange() sont disponinles dans la classe de tests [testOutils](/src/test/java/tests/testOutils/testOutils.java). Ces tests remplissent les scénarios suivants :
* Vérifie getPersonOnRange() entre 0 et 10 ans
* Vérifie getPersonOnRange() entre 10 et 0 ans
* Vérifie l'age max de la liste de personnes (30 est attendu)
* Vérifie l'age max de la liste de personnes si la liste est vide (-1 est attendu par défaut)

## Question 9

Question non prise en compte, EMMA ne fonctionne pas sur IntelliJ avec Java 8. 

## Question 10
Pour nous assurer que les fonctions getPersonsOnRange() et getMaxAge() fonctionnent de manière "anonyme", nous pouvons vérifier que celles-ci n'utilisent pas les fonctions getName() et getFirstName() sur les personnes.
Pour cela, nous pouvons simplement utiliser la fonction vérify sur l'objet mock :
```java
verify(person, atLeastOnce()).getAge(anyObject());
```
Avec cette ligne, nous vérifions que la fonction getAge() est utilisée **au moins une fois** sur l'objet person.

```java
verify(person, never()).getFirstName();
verify(person, never()).getName();
```
Avec ces deux lignes, nous vérifions que les fonctions getFirstName() et getName() **ne sont pas utilisées** sur l'objet person.
