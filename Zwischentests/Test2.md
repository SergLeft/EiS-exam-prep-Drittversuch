Test2:
class Vector3D(val x: Double, val y: Double, val z: Double) {
def dot(other: Vector3D): Double = {
    x * other.x + y * other.y + z * other.z
}


}
1. (3 Punkte) Ergänzen Sie die obenstehende Klasse Vector3D um einen Sekundärkonstruktor, der keine Argumente nimmt und alle drei Vektorkomponenten mit 0 initialisiert.
2. (3 Punkte) Ergänzen Sie die obenstehende Klasse Vector3D um eine Methode, die die Länge des Vektors als Double zurückgibt (∥v∥ =sqrt (v_x^2+v_y^2+v_z^2).
3. (3 Punkte) Ergänzen Sie die obenstehende Klasse Vector3D um eine Methode normalize, die v/∥v∥ zurückgibt, also den Vektor komponentenweise geteilt durch seine Länge. Die Methode soll eine ArithmeticException werfen, wenn die Länge des Vektors 0 ist.
4. (3 Punkte) Welches Verhalten trifft auf den folgenden Code zu?
var vec = Vector3D(0.0, 0.0, 1.0) (mult Choice)
vec.x = 4.0
Der Code kann nicht erfolgreich kompiliert werden.
Der Code wirft einen Fehler zur Laufzeit.
Der Code läuft ohne Fehler und vec.x hat am Ende den Wert 0.0.
Der Code läuft ohne Fehler und vec.x hat am Ende den Wert 4.0.
5. (3 Punkte) Der untenstehende Code verstößt gegen eine zentrale Scala-Stilkonvention. Welche?
@main def main(): Unit = {
    val first_vector = Vector3D(1, 2, 3)
    val second_vector = Vector3D(3, 1, 2)
    println(first_vector.dot(second_vector))
}
