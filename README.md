## TODO-App in React
Erstelle eine einfache ToDo-Liste-Anwendung, in der du Aufgaben hinzufügen, als erledigt markieren und löschen kannst.

Funktionen:
- Eingabefeld zum Hinzufügen neuer Aufgaben.
- Liste der Aufgaben mit Checkboxen zum Markieren als erledigt.
- Löschbutton für jede Aufgabe.
Hinweise:
- Verwende `useState` für die Verwaltung der Aufgaben und des Eingabetextes.
- Überlege, wie du Aufgaben eindeutig identifizieren kannst (z.B. mit einer zufällig generierten ID).
- Nutze Event-Handler für das Hinzufügen von Aufgaben und das Ändern des Erledigungsstatus.
- Beachte, dass alle Daten nur lokal im Browser gespeichert werden und nicht persistent sind, wenn der Browser geschlossen wird.
1. Das Projekt initialisieren
Wir erstellen ein neues React-Projekt mit `create-react-app` und wechseln in das Projektverzeichnis:
```
npx create-react-app todo-app
cd todo-app
```
2. Die Anwendung entwickeln
Wir navigieren in die Hauptkomponente `src/App.js`. Hier ist dann die Hauptlogik der App.
Wir importieren zunäcsht die React-Biblothek mit `import React from 'react';` und die `useState`-Funktion mit `import { useState } from 'react';`. Der `useState`-Hook wird verwendet, um den Zustand der Anwendung zu verwalten. Außerdem wird Stylesheet `App.css` importiert.
```
import React, { useState } from 'react';
import './App.css';
```
Als nächstes definieren wir die Hauptkomponente App mithilfe der Funktion `function App() { ... }`. In dieser Funktion deklarieren wir `todos` als Zustand, der eine leere Liste enthält und `setTodos` als Funktion zum Aktualisieren des Zustands. Die `useState`-Funktion wird verwendet, um den Anfangszustand der Anwendung zu definieren. Zudem deklariert `input` den Zustand für den Texteingabewert. Die `setInput`-Funktion wird verwendet, um den Texteingabewert zu aktualisieren. 
```
function App() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState('');
```
Als nächstes wollen wir Aufgaben hinzufügen. Dazu ertellen wir eine `addTodo`-Funktion, die eine neue Aufgabe erstellt und zur Liste hinzufügt. mit `if(input.trim())` überprüfen wir erstmal, ob der Eingabetext nicht leer ist. Danach werstellen wir mit `const newTodo = ` ein neues Todo-Objekt mit einer zufälligen ID, dem eingegeben Text und einem completed-Flag, das anzeigt, ob die Aufgabe abgeschlossen ist. Danach aktualisierern wir die todos-Liste und fügen das neue Todo-Objekt hinzu.
Mit `setInput('')` wird das Eingabefeld geleert.
```
  const addTodo = () => {
    if (input.trim()) {
      const newTodo = {
        id: Math.random(),
        text: input,
        completed: false
      };
      setTodos([...todos, newTodo]);
      setInput('');
    }
  };
```
Als nächstes wollen wir den Aufgabenstatus ändern. const toggleComplete = (id) => { ... }: Definiert die toggleComplete-Funktion, die den completed-Status einer Aufgabe ändert.
setTodos(todos.map(todo => ... )): Aktualisiert die todos-Liste. Wenn die ID einer Aufgabe mit der angegebenen ID übereinstimmt, wird deren completed-Flag umgekehrt, andernfalls bleibt sie unverändert.
```
  const toggleComplete = (id) => {
    setTodos(
      todos.map(todo =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };
```
Danach wollen wir die Funktion implementieren zum Aufgaben löschen. const deleteTodo = (id) => { ... }: Definiert die deleteTodo-Funktion, die eine Aufgabe löscht.
setTodos(todos.filter(todo => ... )): Aktualisiert die todos-Liste und entfernt die Aufgabe mit der angegebenen ID.
```
  const deleteTodo = (id) => {
    setTodos(todos.filter(todo => todo.id !== id));
  };
```
Dann können wir die Hauptkomponente rendern. 
```
return (
  <div className="App">
    <h1>To-Do Liste</h1>
    <input 
      type="text" 
      value={input} 
      onChange={(e) => setInput(e.target.value)} 
      placeholder="Neue Aufgabe" 
    />
    <button onClick={addTodo}>Hinzufügen</button>
    <ul>
      {todos.map(todo => (
        <li key={todo.id} className={todo.completed ? 'completed' : ''}>
          <input 
            type="checkbox" 
            checked={todo.completed} 
            onChange={() => toggleComplete(todo.id)} 
          />
          {todo.text}
          <button onClick={() => deleteTodo(todo.id)}>Löschen</button>
        </li>
      ))}
    </ul>
  </div>
);

````
Danach müssen wir die App nur noch exportieren.
```
export default App;
```