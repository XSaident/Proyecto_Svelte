<script>
  let newTask = '';
  let tasks = [];

  function addTask() {
    if (newTask.trim()) {
      tasks = [...tasks, { text: newTask, done: false }];
      newTask = '';
    }
  }

  function toggleTask(index) {
    tasks[index].done = !tasks[index].done;
    tasks = [...tasks];
  }

  function deleteTask(index) {
    tasks.splice(index, 1);
    tasks = [...tasks];
  }
</script>

<style>
  :global(body) {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: #f4f4f9;
  }

  header {
    background-color: #4f46e5;
    color: white;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: fixed; 
    top: 0;
    left: 0;
    width: 100%; 
    z-index: 1000;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  }

  .logo {
    font-size: 1.3rem;
    font-weight: bold;
  }

  nav a {
    margin-left: 1.5rem;
    color: white;
    text-decoration: none;
    font-weight: 500;
  }

  nav a:hover {
    text-decoration: underline;
  }

  main {
    padding: 2rem;
    max-width: 600px;
    margin: 5rem auto 2rem; 
    background-color: #fff;
    border-radius: 1rem;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  h1 {
    tex-align: center;
    color: #333;
  }

  .input-container {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
  }

  input {
    flex: 1;
    padding: 0.75rem;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 0.5rem;
  }

  button {
    padding: 0.75rem 1rem;
    font-size: 1rem;
    background-color: #4f46e5;
    color: white;
    border: none;
    border-radius: 0.5rem;
    cursor: pointer;
    transition: background 0.2s;
  }

  button:hover {
    background-color: #4338ca;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  li {
    background: #f0f0ff;
    border: 1px solid #ddd;
    border-radius: 0.5rem;
    margin-bottom: 0.75rem;
    padding: 0.75rem 1rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    transition: background 0.2s;
  }

  li:hover {
    background: #e0e0ff;
  }

  .done {
    text-decoration: line-through;
    color: #888;
  }

  .task-text {
    flex: 1;
    cursor: pointer;
  }

  .delete-btn {
    background: transparent;
    border: none;
    font-size: 1.2rem;
    color: #e11d48;
    cursor: pointer;
  }

  .delete-btn:hover {
    color: #9f1239;
  }
</style>

<header>
  <div class="logo">🗓️ Mi Agenda</div>
  <nav>
    <a href="#">Inicio</a>
    <a hre="#">Fechas Importantes</a>
    <a href="#">Iniciar Sesión</a>
  </nav>
</header>

<main>
  <h1>Tareas Pendientes 🔔</h1>

  <div class="input-container">
    <input
      bind:value={newTask}
      placeholder="Escribe una nueva tarea"
      on:keydown={(e) => e.key === 'Enter' && addTask()}
    />
    <button on:click={addTask}>Agregar</button>
  </div>

  <ul>
    {#each tasks as task, i}
      <li>
        <span
          class:done={task.done}
          class="task-text"
          on:click={() => toggleTask(i)}
        >
          {task.text}
        </span>
        <button class="delete-btn" on:click={() => deleteTask(i)}>🗑️</button>
      </li>
    {/each}
  </ul>
</main>
