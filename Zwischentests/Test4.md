Test4:
class Formatter(private val prefix: String) {
    def format(m: String): String = prefix + m
}
class ErrorFormatter extends Formatter("error: ") {
    def important(m: String): String = format(m).toUpperCase
}

1. (3 Punkte) Betrachten Sie die obenstehenden Klassendefinitionen und die untenstehende main-Methode.
Der Code liefert einen Kompilierfehler. Warum?
@main def main(): Unit = {
    val formatter = Formatter("info - ")
    println(formatter.prefix)
}
2. (3 Punkte) Betrachten Sie die obenstehenden Klassendefinitionen und die untenstehende main-Methode. Was wird am Ende geprintet?
@main def main(): Unit = {
    val formatter = ErrorFormatter()
    val x = formatter.important("bad input")
    println(x)
}
3. (3 Punkte) Was würde mit dem Programm aus Aufgabe 2 passieren, wenn man bei format in der Klasse Formatter das Schlüsselwort protected ergänzt (also protected def format(m: String) usw.)? (Mult choice)
Das Programm kann nicht mehr kompiliert werden.
Das Programm ist weiterhin kompilierbar, beim Aufruf von format st¨urzt das Programm ab.
Das Programm ist weiterhin kompilierbar, beim Aufruf von important st¨urzt das Programm ab.
Das Programm ist weiterhin kompilierbar und produziert die gleiche Ausgabe.
4. (3 Punkte) Eine Scala-Klasse A ist mit dem Schl¨usselwort abstract markiert. Welche zwei Aussagen sind korrekt? (mult choice)
Methoden in A dürfen ohne Implementierung deklariert werden.
Jede Klasse, die von A erbt, muss ebenfalls immer mit abstract markiert sein.
Keine Klasse darf von A erben.
Es können keine Instanzen der Klasse A angelegt werden.
5. (3 Punkte) Nennen Sie einen Unterschied zwischen den Klassen HashIndex und TreeIndex aus der Vorlesung
