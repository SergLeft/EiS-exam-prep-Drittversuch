Klausur SoSe23

1. Transformationen (20 Punkte)
In dieser Aufgabe betrachten wir ein Job-Portal, in dem Programmierer ihre Expertise
in verschiedenen Programmiersprachen veröffentlichen können. Ein Programmierer
wird durch die folgende Klasse modelliert:
case class Programmer(
    firstName: String,
    lastName: String,
    age: Int,
    experienceYears: Map[String, Int]
)
Den Programmierer Mardo Rossky, 44 Jahre alt, mit 9 Jahren Erfahrung in Scala und
17 Jahren Erfahrung in Python würde man dann so darstellen:

Programmer("Mardo", "Rossky", 44, Map("Python" -> 17, "Scala" -> 9))

Sie können davon ausgehen, dass alle Jahresangaben strikt positiv sind.
Die Klasse Applicants speichert eine Sammlung von Bewerbern in der Variable ps und
soll verschiedene Hilfsfunktionen ausführen. Implementieren Sie dazu in der Vorlage
auf der nächsten Seite die folgenden Methoden:
(a) (5 Punkte) lastNameStartsWith nimmt eine Zeichenkette entgegen und soll alle
Bewerber zurückgeben, deren Nachname mit dieser Zeichenkette beginnt. Dabei
soll Groß- und Kleinschreibung ignoriert werden!
(b) (5 Punkte) scalaExpert gibt den Bewerber mit der meisten Erfahrung in Scala
zurück. Wenn es mehrere gibt, reicht es, einen davon zurückzugeben. Wenn kein
Bewerber Erfahrung mit Scala hat, soll None zurückkommen.
(c) (5 Punkte) subjectsCovered gibt eine Auflistung aller Programmiersprachen zu-
rück, die von mindestens einem Bewerber beherrscht werden. Die Auflistung soll
keine Duplikate enthalten.
(d) (5 Punkte) Einige Bewerber versuchen ihre Chancen zu erhöhen, indem sie eine
sehr große Zahl an Erfahrungsjahren angeben. Die Methode dishonest gibt die
Bewerber zurück, die in mindestens einer Programmiersprache mehr Erfahrungs-
jahre als ihr eigenes Alter angegeben haben.

class Applicants(val ps: Seq[Programmer]) {
    def lastNameStartsWith(prefix: String): Iterable[Programmer] =
    def scalaExpert: Option[Programmer] =
    def subjectsCovered: Iterable[String] =
    def dishonest: Iterable[Programmer] =

}

2. Typinferenz (14 Punkte)
Im untenstehenden Scala-Codebeispiel werden unveränderliche Variablen deklariert,
ohne deren Datentyp explizit anzugeben. In diesem Fall bestimmt der Scala-Compiler
die Datentypen automatisch.
1 def makePartitions ( elems : Int , parts : Int ) = {
2 (0 until parts )
3 . map (i => ( elems * i / parts , elems * (i + 1) / parts ))
4 . to ( ArraySeq )
5 }
6
7 @main def inference (): Unit = {
8 val v0 = " Viel Erfolg !"
9 val v1 = v0 . size
10 val v2 = ArraySeq (2.2 , 3.3 , 4.4)
11 val v3 = (i: Int , j: Int ) => v2 (i) < v2 (j)
12 val v4 = makePartitions
13 }
Beantworten Sie die untenstehenden Fragen. Beachten Sie, dass Datentypen immer
vollständig inferiert werden, beispielsweise List[Float] statt nur List. Als Antworten
werden daher nur vollständige Datentypen akzeptiert.
(a) (2 Punkte) Welcher Scala-Datentyp wird für v0 inferiert? Begründen Sie kurz.
(b) (2 Punkte) Welcher Scala-Datentyp wird für v1 inferiert? Begründen Sie kurz.
(c) (2 Punkte) Welcher Scala-Datentyp wird für v2 inferiert? Begründen Sie kurz.
(d) (2 Punkte) Welcher Scala-Datentyp wird für v3 inferiert? Begründen Sie kurz.
(e) (3 Punkte) Welcher Scala-Datentyp wird für v4 inferiert? Begründen Sie kurz.
(f) (3 Punkte) Was ist der Rückgabewert (nicht Rückgabetyp!) des Aufrufs v4(9, 3)?

3. Auflösung von Aufrufen (18 Punkte)
Betrachten Sie den folgenden Scala-Codeausschnitt und beantworten Sie dann die un-
tenstehenden Fragen.
1 abstract class AnnotatedOutput {
2     protected def annotation : String = " > >"
3     protected def output (s: String ): Unit = println (s)
4     def outputAnnotated ( something : Any ): Unit = {
5         output ( annotation + something . toString )
6     }
7 }
8
9 class CustomAnnotation ( ann : String ) extends AnnotatedOutput {
10    override protected def annotation : String = ann
11 }
12
13 class LoggedOutput extends AnnotatedOutput {
14     private val log : ArrayBuffer [ String ] = ArrayBuffer ()
15     override protected def output (s: String ): Unit = log . append (s)
16     def getLog : ArraySeq [ String ] = log . to ( ArraySeq )
17 }
18
19 @main def main (): Unit = {
20     val p1 : AnnotatedOutput = CustomAnnotation (" main : ")
21     val p2 : LoggedOutput = LoggedOutput ()
22     val p3 : AnnotatedOutput = p2
23
24 p1 . outputAnnotated (" message1 ") // (1)
25 p2 . outputAnnotated (" message2 ") // (2)
26 p3 . outputAnnotated (" message3 ") // (3)
27 println ( p2 . getLog ) // (4)
28 }
(a) (4 Punkte) Was wird in der durch (1) markierten Zeile geprintet? Begründen Sie!
(b) (4 Punkte) Was wird in der durch (2) markierten Zeile geprintet? Begründen Sie!
(c) (4 Punkte) Was wird in der durch (3) markierten Zeile geprintet? Begründen Sie!
(d) (4 Punkte) Was wird in der durch (4) markierten Zeile geprintet? Begründen Sie!
(e) (2 Punkte) Ist das Programm kompilierbar, wenn am Ende der main-Methode ei-
ne Zeile println(p3.getLog) hinzugefügt wird? Begründen Sie kurz!

4. Unendliche Iteration (20 Punkte)
Bisher haben wir nur endliche Sequenzen betrachtet, zum Beispiel ArraySeq[A]. Mit
dem Trait Iterable[A] können wir aber auch unendliche Sequenzen darstellen. Der
Inhalt der Sequenz wird dabei nicht explizit gespeichert, sondern während der Iteration
berechnet. Die Scala-Definition von Iterable[A] und Iterator[A] finden Sie auf der
letzten Seite der Klausur.
(a) (8 Punkte) Implementieren Sie die untenstehende Klasse InfiniteCounter. Der
Iterator soll nach der Erstellung bei 0 starten und in jedem Schritt die nächste
natürliche Zahl zurückgeben, also die Sequenz 0, 1, 2, 3, . . ..
(b) (12 Punkte) Jetzt wollen wir eine interessantere Anwendung betrachten: Uns wird
eine Funktion f: Long => Double vorgegeben. f nimmt also eine ganze Zahl ent-
gegen und gibt eine reelle Zahl zurück. Daraus kann man eine unendliche Sequenz
der Partialsummen von f konstruieren:
f (0), f (0) + f (1), f (0) + f (1) + f (2), f (0) + f (1) + f (2) + f (3), . . .
Beispiel: f (i) = 2i + 1 erzeugt die Sequenz 1.0, 4.0, 9.0, 16.0, . . .
Implementieren Sie diese unendliche Sequenz in der Klasse Series auf der nächs-
ten Seite. Die Funktion f wird im Konstruktor übergeben. Der Iterator soll die
Einträge der Sequenz einzeln und nacheinander zurückgeben.
class InfiniteCounter extends Iterable[Long] {
    def iterator: Iterator[Long] =

}

class Series(f: Long => Double) extends Iterable[Double] {
    def iterator: Iterator[Double] =

}

5. Einheitensystem der Freiheit (15 Punkte)
Im englischsprachigen Raum werden Körpergrößen häufig noch in Fuß (feet/ft) und
Zoll (inches/in) angegeben. 1 Fuß entspricht genau 12 Zoll. Die Zoll-Angabe wird
folglich immer so gewählt, dass sie zwischen 0 und 11 liegt, und es wird immer auf die
nächste Ganzzahl gerundet. Man würde also niemals “5 feet 14 inches” sagen, sondern
nur “6 feet 2 inches”.
Weiter unten finden Sie den Anfang einer Klasse ImperialHeight, mit der diese Grö-
ßenangabe modelliert werden soll. Ergänzen Sie der Klasse folgende Funktionalität:
(a) (3 Punkte) Der Konstruktor soll eine IllegalArgumentException werfen, wenn
die Fuß- oder Zoll-Angabe negativ ist. Diese Exception soll auch geworfen wer-
den, wenn inches größer als 11 ist.
(b) (4 Punkte) Implementieren Sie eine Methode def modify(deltaInches: Int).
Die Methode soll eine neue ImperialHeight zurückgeben, die um die übergebene
Zoll-Anzahl erhöht wurde. deltaInches darf negativ sein, aber die zurückgegebe-
ne ImperialHeight nicht. Werfen Sie in diesem Fall eine IllegalArgumentException.
(c) (3 Punkte) Überschreiben Sie equals und hashCode für ImperialHeight, damit
zwei Instanzen auf strukturelle Gleichheit getestet werden können.
(d) (2 Punkte) Überschreiben Sie toString. Die String-Repräsentation für
ImperialHeight(6, 2) soll folgendermaßen aussehen: "6 ft 2 in"
(e) (3 Punkte) Implementieren Sie im Companion-Objekt eine Methode
def fromInches(in: Int): ImperialHeight, die eine Größe in Zoll entgegen-
nimmt und diese in eine ImperialHeight umrechnet. Wenn die übergebene Größe
negativ ist, soll eine IllegalArgumentException geworfen werden.
class ImperialHeight(val feet: Int, val inches: Int)

6. Sortierung (12 Punkte)
Schauen Sie sich die Definition der Klasse Person an. Die Definition von ImperialHeight
finden Sie in der vorigen Aufgabe.
case class Person(name: String, height: ImperialHeight)
Ergänzen Sie jetzt die zwei untenstehenden Methoden:
(a) (6 Punkte) sortPersonsByHeight nimmt eine Sequenz von Personen gibt eine
neue Sequenz zurück, in der die Personen aufsteigend nach ihrer Körpergröße
geordnet sind.
(b) (6 Punkte) findLargestPersonWithName nimmt eine Sequenz von Personen und
gibt die größte Person mit dem übergebenen Namen zurück. Wenn keine derartige
Person existiert, soll None zurückgegeben werden. Wenn mehrere Personen das
Kriterium erfüllen, soll irgendeine davon zurückgegeben werden.
def sortPersonsByHeight(s: Seq[Person]): Seq[Person] =
def findLargestPersonWithName(name: String, s: Seq[Person]): Option[Person] =


7. Verzögerte Auswertung (21 Punkte)
In einer normalen Map[K, V] lassen sich Schlüssel-Wert-Paare mit updated einfügen
und mit removed löschen. In manchen Situationen bietet es sich an, sich die Änderun-
gen vorzumerken: Wir hinterlegen also, dass eine Änderung stattgefunden hat, ohne
diese auf die eigentliche Map[K, V] anzuwenden. Dazu verwenden wir folgenden Da-
tentyp:
/** Repräsentiert vorgemerkte Änderungen in einer [[Map]]. */
trait Changes[K, V]
/** Speichert eine Map, bei der noch keine Änderungen vorgemerkt wurden. */
case class Unchanged[K, V](map: Map[K, V]) extends Changes[K, V]
/** Bedeutet, dass in `base` das Paar `(key, newValue)` eingefügt werden soll. */
case class Modify[K, V](key: K, newValue: V, base: Changes[K, V]) extends Changes[K, V]
/** Bedeutet, dass in `base` der Schlüssel `key` gelöscht werden soll. */
case class Delete[K, V](key: K, base: Changes[K, V]) extends Changes[K, V]
Schauen Sie sich zum besseren Verständnis das folgende Anwendungsbeispiel an:
@main def testChanges(): Unit = {
    val someMap: Map[String, Int] = HashMap("x" -> 20, "y" -> 50, "z" -> 100)
    val noChanges: Changes[String, Int] = Unchanged(someMap)
    val withDelete: Changes[String, Int] = Delete("x", noChanges)
    val withUpdate: Changes[String, Int] = Modify("z", 10, withDelete)
    println(containsKey("x", withUpdate)) // output: false
    println(getValueForKey("x", withUpdate)) // output: None
    println(getValueForKey("y", withUpdate)) // output: Some(50)
    println(getValueForKey("z", withUpdate)) // output: Some(10)
    println(toMap(withUpdate)) // output: HashMap(y -> 50, z -> 10)
}
Vervollständigen Sie dann die drei folgenden Methoden (auf dieser und nächster Seite)
für Changes[K, V] anhand ihrer Scaladoc-Kommentare.
/** Prüft, ob ein gegebener Schlüssel nach Anwendung der
* vorgemerkten Änderungen vorhanden ist.
*
* @param searchKey der Schlüssel, nach dem gesucht wird
* @param map die Map mit vorgemerkten Änderungen, in der gesucht wird
* @return true, wenn der Schlüssel vorhanden ist, sonst false
*/
def containsKey[K, V](searchKey: K, map: Changes[K, V]): Boolean =
/** Gibt den Wert zurück, der zum übergebenen Schlüssel gehört.
*
* @param searchKey der Schlüssel, nach dem gesucht wird
* @param map die Map mit vorgemerkten Änderungen, in der gesucht wird
* @return den zugehörigen Wert, falls der Schlüssel vorhanden ist, sonst None
*/
def getValueForKey[K, V](searchKey: K, map: Changes[K, V]): Option[V] =
/** Wendet alle vorgemerkten Änderungen an.
*
* @param map eine Map mit eventuell vorgemerkten Änderungen
* @return eine Map, in der alle Änderungen durchgeführt wurden
*/
def toMap[K, V](map: Changes[K, V]): Map[K, V] =
