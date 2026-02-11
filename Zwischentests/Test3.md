Test3:
1. (3 Punkte) Was beschreibt der Begriff “Methode höherer Ordnung”? (Mult choice)
Eine Methode ohne Argumente
Eine Methode ohne Seiteneffekte
Eine Methode, die eine oder mehrere Funktionen als Argumente nimmt
Eine Methode in alphabetischer Reihenfolge innerhalb der Scala-Datei
2. (3 Punkte) Welchen Datentyp inferiert Scala für die Variable v1? (Mult Choice)
val v1 = ArraySeq(3.14, 2.71, 1.6)
Double, ArraySeq[Double], (Double, Double, Double), Unit
3. (3 Punkte) Welchen Datentyp inferiert Scala für die Variable v2? (mult choice)
val v2 = (s: String) => s.size != 16
String, Boolean, String => Boolean, String => Int
4. (3 Punkte) Welchen Wert hat die Variable desc nach Ausführung der folgenden Zeilen?
val num = 4
val desc = num match {
    case 0 => "nothing"
    case 1 => "one apple"
    case _ => num + " apples"
}
5. (3 Punkte) Ergänzen Sie die untenstehende Funktion so, dass sie zurückgibt, wie viele der übergebenen Zeichenketten mehr als 3 Zeichen haben.
Beispiel: countLongStrings(ArraySeq("x", "abcde", "eis")) soll 1 zurückgeben.
def countLongStrings(input: ArraySeq[String]): Int =
