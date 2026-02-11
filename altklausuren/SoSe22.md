Klausur SoSe22

1. Auflösung von Aufrufen (15 Punkte)
Der untenstehende Scala-Codeausschnitt gibt 3 Zeilen auf der Standardausgabe aus.
Sie sollen in dieser Aufgabe den ausgegebenen Text ermitteln.
1 class BaseClass {
2 def printMe (): Unit = println (" base class ")
3 }
4 class DerivedClass extends BaseClass {
5 override def printMe (): Unit = println (" derived class ")
6 }
7 class SecondDerivedClass extends BaseClass
8
9 def printThat ( something : BaseClass ): Unit = {
10 something . printMe ()
11 }
12 def performAction ( something : DerivedClass ): Unit = {
13 println (" derived action ")
14 }
15 def performAction ( something : SecondDerivedClass ): Unit = {
16 println (" another derived action ")
17 }
18
19 @main def main (): Unit = {
20 val x = DerivedClass ()
21 val y = SecondDerivedClass ()
22 performAction (y)
23 printThat (x)
24 printThat (y)
25 }
(a) (5 Punkte) Was steht in der ersten Zeile der Ausgabe? Begründen Sie kurz.
(b) (5 Punkte) Was steht in der zweiten Zeile der Ausgabe? Begründen Sie kurz.
(c) (5 Punkte) Was steht in der dritten Zeile der Ausgabe? Begründen Sie kurz.


2. Typkonvertierung und Typinferenz (12 Punkte)
Im untenstehenden Scala-Codebeispiel werden unveränderliche Variablen deklariert,
ohne deren Datentyp explizit anzugeben. In diesem Fall bestimmt der Scala-Compiler
die Datentypen automatisch.
1 def doubleMe (i: Long ) = i * 2
2
3 @main def inference (): Unit = {
4 val one = " one "
5 val two = doubleMe (10)
6 val three = (" three ", (4.2 , 13.37))
7 val four = ArraySeq (" hi ", " bye ", "x "). map (s => s. size )
8 val five = (x: Double , y: Double ) => x * x + y * y
9 val six = five (2 , 4.2)
10 }
Geben Sie für alle sechs Variablen an, welcher Datentyp inferiert wird, inklusive ei-
ner kurzen Begründung. Beachten Sie, dass Datentypen immer vollständig inferiert
werden, beispielsweise List[Float] statt nur List. Als Antworten werden daher nur
vollständige Datentypen akzeptiert.
(a) (2 Punkte) Welcher Scala-Datentyp wird für one inferiert? Begründen Sie kurz.
(b) (2 Punkte) Welcher Scala-Datentyp wird für two inferiert? Begründen Sie kurz.
(c) (2 Punkte) Welcher Scala-Datentyp wird für three inferiert? Begründen Sie kurz.
(d) (2 Punkte) Welcher Scala-Datentyp wird für four inferiert? Begründen Sie kurz.
(e) (2 Punkte) Welcher Scala-Datentyp wird für five inferiert? Begründen Sie kurz.
(f) (2 Punkte) Welcher Scala-Datentyp wird für six inferiert? Begründen Sie kurz.


3. Versteckter Fehler (18 Punkte)
Der untenstehende Scala-Codeausschnitt soll den Score einer Web-Adresse in einer
HashMap bekannter Web-Adressen abfragen. Der Code kompiliert ohne Probleme, lie-
fert aber bei der Ausführung ein falsches Ergebnis: Obwohl für den Programmierer
sofort ersichtlich ist, dass die angefrage Adresse in der HashMap vorkommt, gibt der
Scala-Code trotzdem den Wert None aus.
1 class WebAddress ( val hostName : String , val port : Int ) {
2 if ( port < 0 || port > 65535)
3 throw IllegalArgumentException (" illegal port ")
4 }
5
6 @main def checkTrusted (): Unit = {
7 val trustScores = HashMap [ WebAddress , Double ](
8 WebAddress (" uni - mainz . de ", 80) -> 1000 ,
9 WebAddress (" google . com ", 443) -> 40 ,
10 WebAddress (" aws . amazon . com ", 22) -> 70 ,
11 WebAddress (" twitter . com ", 443) -> 0
12 )
13
14 val address = WebAddress (" uni - mainz . de ", 80)
15 println ( trustScores . get ( address ))
16 }
(a) (5 Punkte) Erklären Sie, wieso die angefragte Web-Adresse nicht gefunden wird.
(b) (10 Punkte) Welche Veränderungen an WebAddress müsste man vornehmen, da-
mit der Code wie erwartet funktioniert? Implementieren Sie eine Variante von
WebAddress mit den nötigen Änderungen!
(c) (3 Punkte) Was passiert, wenn man im gegebenen Codebeispiel TreeMap statt
HashMap schreibt?

4. Operationen auf Intervallen (20 Punkte)
Der folgende Scala-Code zeigt eine einfache Klasse, die ein abgeschlossenes Intervall
(closed interval) repräsentiert. Ein abgeschlossenes Intervall [a, b] enthält alle Werte
zwischen der unteren Grenze a und der oberen Grenze b, inklusive der Grenzen selbst,
d.h. x ∈ [a, b] genau dann, wenn a ≤ x ≤ b.
1 /** Abgeschlossenes Intervall
2 * @constructor Erzeugt ein neues abgeschlossenes Intervall
3 * @param lo untere Grenze
4 * @param hi obere Grenze
5 */
6 class CInterval ( val lo : Long , val hi : Long ) {
7 def contains ( value : Long ): Boolean = lo <= value && value <= hi
8 def isEmpty : Boolean = lo > hi
9 }
Vervollständigen Sie die folgenden vier Methoden. Alle Methoden sind außerhalb der
Klasse definiert.
(a) (5 Punkte) countContained soll zurückgeben, wie viele der übergebenen Werte
im übergebenen Intervall liegen.
def countContained(interval: CInterval, values: Seq[Long]): Int =
(b) (5 Punkte) getSizes soll für jedes der übergebenen Intervalle die Intervallgröße
zurückgeben.
Beispiel: [9, 11] hat Größe 3, da es drei Werte enthält, nämlich 9, 10, und 11.
def getSizes(intervals: Seq[CInterval]): Seq[Long] =

(c) (5 Punkte) boundingInterval soll ein Intervall konstruieren, das alle übergebe-
nen Werte enthält. Wenn die Eingabesequenz leer ist, darf ein beliebiges Intervall
zurückgegeben werden.
def boundingInterval(values: Seq[Long]): CInterval =
(d) (5 Punkte) firstToContainAll gibt das erste Intervall aus der übergebenen Se-
quenz zurück, das alle übergebenen Werte enthält. Falls kein Intervall diese Be-
dingung erfüllt, soll None zurückgegeben werden.
def firstToContainAll(
intervals: Seq[CInterval],
values: Seq[Long]): Option[CInterval] =


5. Interaktion mit Traits (20 Punkte)
In Scala ist es in vielen Fällen gar nicht notwendig, die konkrete Implementierung eines
Traits zu kennen, um damit zu programmieren. Für diese Aufgabe werden Ihnen die
folgenden Traits und Hilfsmethoden vorgegeben:
1 /** Ein Wegpunkt entlang eines Pfades . */
2 trait Waypoint {
3 /** Gibt den Namen des Wegpunktes zur ü ck . */
4 def name : String
5 /** Gibt die Koordinaten des Wegpunktes zur ü ck . */
6 def coordinates : Coordinates3D
7 }
8
9 /** Ein Punkt in einem kartesischen Koordinatensystem . */
10 trait Coordinates3D {
11 /** Gibt die x - Koordinate zur ü ck . */
12 def x: Double
13 /** Gibt die y - Koordinate zur ü ck . */
14 def y: Double
15 /** Gibt die Hö he (z - Koordinate ) zur ü ck . */
16 def elevation : Double
17 }
18
19 /** Eine Streckenl ä nge . */
20 trait Distance {
21 /** Gibt die Distanz in Metern zur ü ck . */
22 def toMeters : Double
23 /** Gibt die Distanz in englischen Meilen zur ü ck . */
24 def toMiles : Double
25 }
26
27 /** Ein Distanzma ß zwischen zwei Objekten vom Typ A. */
28 trait DistanceFunction [A] {
29 /** Gibt die Distanz zwischen zwei Objekten zur ü ck . */
30 def apply ( from : A , to : A ): Distance
31 }
32
33 /** Bildet Paare aus aufeinanderfolgenden Elementen .
34 *
35 * pairwise ( Seq (1 , 2, 3)) -> Seq ( (1 , 2) , (2 , 3) )
36 */
37 def pairwise [A ]( input : Seq [A ]): Seq [(A , A )] = input . zip ( input . tail )
(a) (15 Punkte) Ergänzen Sie die Funktionskörper der folgenden zwei Methoden.
Halten Sie sich an die Vorgaben in den Scaladoc-Kommentaren!
/** Gibt den Namen eines Wegpunktes mit maximaler Höhe zurück,
falls dieser in der Eingabe existiert, ansonsten None. */
def maxElevationWaypoint(waypoints: Seq[Waypoint]): Option[String] =

/** Berechnet die Gesamtlänge des Pfades entlang der gegebenen Wegpunkte in Metern.
*
* @param path die Wegpunkte, aus denen sich der Pfad zusammensetzt.
* @param df die Distanzfunktion, mit der die Abstände berechnet werden.
* @return die Gesamtlänge des Pfades in Metern.
* @throws IllegalArgumentException wenn der Pfad keine Wegpunkte enthält.
*/
def findPathLengthMeters(
path: Seq[Waypoint],
df: DistanceFunction[Coordinates3D]): Double =
(b) (5 Punkte) Schreiben Sie eine eigene Klasse, die von Waypoint ableitet und den
Wegpunktnamen sowie die Koordinaten als unveränderliche Felder speichert. Es
soll außerdem möglich sein, den Namen und die Koordinaten als Konstruktorargumente zu übergeben.


6. Erweiterter Zahlenraum (15 Punkte)
Für manche Anwendungen ist es nützlich, dass Zahlen auch unendlich groß sein kön-
nen. In Scala lassen sich zwar sehr große Zahlen als Long darstellen, aber nicht die
Werte ±∞. Stattdessen können wir einen eigenen Datentypen mittels enum definieren:
1 enum ExtendedLong {
2 case PosInf
3 case NegInf
4 case Finite (i: Long )
5 }
Der Datentyp ExtendedLong lässt eine offensichtliche Sortierung zu: −∞ ist kleiner
als jeder andere Wert (außer −∞), und +∞ ist größer als jeder andere Wert (außer
+∞). Dadurch ergibt sich z.B. die Sortierung −∞ < −42 < 0 < 2 < +∞, bzw.
NegInf < Finite(-42) < Finite(0) < Finite(2) < PosInf.
Schreiben Sie eine Scala-Klasse, die von Ordering[ExtendedLong] erbt, und die oben
beschriebene Sortierung implementiert. Die Definition von Ordering finden Sie auf
der letzten Seite der Klausur. Der Anfang ist bereits vorgegeben:
// Erlaubt es, z.B. PosInf statt ExtendedLong.PosInf zu schreiben
import ExtendedLong.*
class ExtendedLongOrdering extends Ordering[ExtendedLong]


7. Parametrisierte Datentypen (20 Punkte)
Ein Array ist eine Datenstruktur fester Größe mit durchnummerierten Einträgen
(bei 0 beginnend), die einen schnellen Zugriff auf jeden beliebigen Einträg ermög-
licht.
Wenn ein Großteil der Array-Einträge einen einzelnen, festen Standardwert D an-
nimmt, spricht man von einem dünn besetzten Array (englisch sparse array). Dünn be-
setzte Arrays lassen sich effizienter speichern, indem man sich nur die Einträge merkt,
die nicht den Wert D annehmen (z.B. mit einer HashMap).
Beispiele für dünn besetzte Arrays:
0 0 5 0 0 0 0 0 3 (Größe 9, D = 0)
x # # # # y # # # # # z # # # (Größe 15, D = #)
(a) (15 Punkte) Ergänzen Sie die Vorlage auf der nächsten Seite, um ein dünn be-
setztes Array zu implementieren. Denken Sie daran, dass der Standardwert nie in
der Map gespeichert werden soll, und halten Sie sich außerdem an die Vorgaben
in den Scaladoc-Kommentaren!
(b) (5 Punkte) Sorgen Sie dafür, dass eine IllegalArgumentException geworfen wird,
wenn ein negativer Wert für die Größe übergeben wird

/** Ein dünn besetztes Array.
*
* @constructor Erzeugt ein neues Array mit der übergebenen Größe.
* @param size die feste Größe dieses Arrays
* @param default der Standardwert D für dieses Array
*/
class MutableSparseArray[A](val size: Int, val default: A) {
// bildet die Arrayposition auf den jeweiligen Wert ab
private val entries = mutable.HashMap[Int, A]()
/** Gibt zurück, welches Element an der übergebenen Position gespeichert ist.
*
* @throws IndexOutOfBoundsException wenn die Position im Array nicht existiert
*/
def apply(position: Int): A =
/** Schreibt den übergebenen Wert an die übergebene Position im Array.
*
* @throws IndexOutOfBoundsException wenn die Position im Array nicht existiert
*/
def update(position: Int, value: A): Unit =
/** Gibt eine Sequenz mit allen Einträgen dieses Arrays zurück,
inklusive der nicht explizit gespeicherten Standardwerte. */
def asDense: Seq[A] =
/** Gibt eine Zeichenkette mit allen Einträgen dieses Arrays zurück,
inklusive der nicht explizit gespeicherten Standardwerte. */
override def toString: String =
}

