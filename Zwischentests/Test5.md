Test5:
// Stockwerk und Raumnummer
class Room(val level: Int, val number: Int)
class Formatter {
    def format(r: Room): String = "some room"
}
class SeparatedFormatter(sep: String) extends Formatter {
    def separator: String = sep
    override def format(r: Room): String = r.level + separator + r.number
}
@main def main(): Unit = {
    val r1 = Room(3, 225)
    val r2 = Room(4, 120)
    val f1: Formatter = Formatter()
    val f2: Formatter = SeparatedFormatter("-")
    println(f1.format(r1)) // (1)
    println(f2.format(r2)) // (2)
}

1. (3 Punkte) Schreiben Sie eine Klasse NoLevelFormatter, die von Formatter erbt und in format nur dieRaumnummer zusammen mit dem Präfix “Raum” zurückgibt. Beispiel: r1 wird zu "Raum 225".
2. (3 Punkte) Sie führen println(r1 == Room(3, 225)) in der main-Methode aus. Es wird false geprintet, was offensichtlich nicht korrekt ist. Wie kann dieser Fehler behoben werden?
3. (3 Punkte) Was wird in der mit (1) markierten Zeile geprintet?
4. (3 Punkte) Was wird in der mit (2) markierten Zeile geprintet?
5. (3 Punkte) Wir fügen jetzt Zeile println(f2.separator) am Ende der main-Methode ein. Warum führt das zu einem Kompilierfehler, obwohl SeparatedFormatter die Methode separator definiert?
