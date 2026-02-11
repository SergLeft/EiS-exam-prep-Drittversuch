Test6:
trait History[A]
case class Append[A]() extends History[A]
case class Update[A](index: Int, oldEntry: A) extends History[A]
class UndoArray[A] {
    private val array = mutable.ArrayBuffer[A]()
    private var lastChange: Option[History[A]] = None
    def append(newEntry: A): Unit = {
        array.append(newEntry)
        lastChange = Some(Append())
}
def update(index: Int, newEntry: A): Unit = ???
def undoLast(): Unit = lastChange match {
    case None => throw IllegalStateException("cannot undo")
    case Some(Update(index, old)) =>
        array.update(index, old)
        lastChange = None
    case Some(Append()) =>
        array.dropRightInPlace(1) // deletes last element
        lastChange = None
    }
}

Die Klasse UndoArray[A] repräsentiert eine Array-ähnliche Datenstruktur, in der die zuletzt ausgeführte Operation rückgängig gemacht werden kann.
1. (3 Punkte) Unten wird ein neues UndoArray[Int] angelegt. Ergänzen Sie zusätzlichen Scala-Code, der nacheinander eine 2 und eine 6 anhängt und danach die letzte Operation rückgängig macht.
val arr = UndoArray[Int]()
2. (3 Punkte) Was passiert, wenn man undoLast auf ein neu erstelltes (leeres) UndoArray aufruft? (mult choice)
Nichts.
Das Programm wirft eine IllegalStateException.
Das Programm wirft eine NoSuchElementException.
3. (3 Punkte) Warum ist es notwendig, das Feld lastChange als var (und nicht als val) zu deklarieren?
4. (3 Punkte) Wie würde man in der Klasse UndoArray[A] eine Methode size implementieren, die die Anzahl der gespeicherten Elemente zurückgeben soll? (mult choice)
def size: Int = this.size
override def size: Int = array.size
def size: Int = array.size
val size: Int = array.size
5. (3 Punkte) Ergänzen Sie (rechts neben dem Scala-Code oben) die fehlende Implementierung von update, die den Eintrag an der übergebenen Position durch den übergebenen Eintrag austauschen soll. Bedenken Sie, dass es möglich sein soll, diese Operation mit undoLast rückgängig zu machen
