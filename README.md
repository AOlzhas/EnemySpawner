# EnemySpawner

### **Пошаговое руководство по созданию CharacterSpawnController в Unity на C#**

#### **Шаг 1: Создайте проект в Unity**
1. Откройте **Unity Hub** и создайте новый **3D-проект**.
2. Перейдите в **Assets > Create > Folder** и назовите его **Scripts**.
3. В этом **Scripts**-папке создайте новый **C#-скрипт**:
   - Нажмите **ПКМ (Правой Кнопкой Мыши) > Create > C# Script**.
   - Назовите его **CharacterSpawnController**.

---

#### **Шаг 2: Открытие и настройка скрипта CharacterSpawnController**
1. Дважды кликните **CharacterSpawnController.cs**, чтобы открыть его в **Visual Studio** или **Rider**.
2. Очистите шаблонный код и вставьте следующий код:

```csharp
using System.Collections;
using UnityEngine;

public class CharacterSpawnController : MonoBehaviour
{
    public GameObject enemyPrefab; // Префаб врага
    public Transform[] spawnPoints; // Точки спавна врагов
    public float spawnInterval = 5f; // Интервал спавна врагов
    private int maxEnemies = 5; // Начальное количество врагов
    private int currentEnemies = 0; // Текущее количество врагов
    private float elapsedTime = 0f; // Прошедшее время

    private void Start()
    {
        StartCoroutine(SpawnEnemies());
        StartCoroutine(IncreaseMaxEnemiesOverTime());
    }

    private IEnumerator SpawnEnemies()
    {
        while (true)
        {
            yield return new WaitForSeconds(spawnInterval);

            if (currentEnemies < maxEnemies)
            {
                SpawnEnemy();
            }
        }
    }

    private void SpawnEnemy()
    {
        if (spawnPoints.Length == 0) return;

        Transform spawnPoint = spawnPoints[Random.Range(0, spawnPoints.Length)];
        Instantiate(enemyPrefab, spawnPoint.position, spawnPoint.rotation);
        currentEnemies++;
    }

    private IEnumerator IncreaseMaxEnemiesOverTime()
    {
        while (true)
        {
            yield return new WaitForSeconds(60f); // Каждую минуту увеличиваем лимит
            maxEnemies++;
        }
    }
}
```

---

#### **Шаг 3: Добавление спавнера в сцену**
1. В **Unity** создайте пустой объект:  
   - **GameObject > Create Empty**, назовите его **EnemySpawner**.
   - Перетащите на него скрипт **CharacterSpawnController**.
   
2. Добавьте точки спавна:  
   - Создайте **несколько пустых объектов** (GameObject) в сцене.  
   - Назовите их **SpawnPoint_1, SpawnPoint_2, ...**  
   - Разместите их в разных местах карты.  
   - В **EnemySpawner** в поле **Spawn Points** добавьте эти точки.

---

#### **Шаг 4: Подготовка префаба врага**
1. **Создайте врага**:
   - Добавьте **3D Object > Capsule** или **Cube**.
   - Назовите его **Enemy**.
   - Добавьте **Component > Rigidbody** (убедитесь, что галочка **Use Gravity** включена).
   - Добавьте **Component > Capsule Collider** (если нужен коллайдер).
   - Перетащите **Enemy** в папку **Prefabs** (создайте ее, если ее нет).
   - Удалите **Enemy** из сцены, оставив его как префаб.

2. В **EnemySpawner** перетащите **Enemy Prefab** в **поле Enemy Prefab**.

---

#### **Шаг 5: Запуск сцены и тестирование**
1. Запустите игру, и **каждые 5 секунд** должны появляться новые враги.
2. Каждую минуту лимит врагов будет увеличиваться.

---

#### **Шаг 6: Добавление проекта в GitHub**
1. Откройте **Git Bash (или терминал)** в папке проекта.
2. Введите команды:

```sh
git init
git add .
git commit -m "Initial commit with CharacterSpawnController"
git branch -M main
git remote add origin https://github.com/ВАШ_АККАУНТ/ВАШ_РЕПОЗИТОРИЙ.git
git push -u origin main
```

3. **Дайте доступ**:
   - Перейдите в **Settings > Collaborators** на GitHub.
   - Добавьте моего GitHub-аккаунт.

---

Теперь ваш **спавнер врагов готов**! Если что-то не работает, спрашивайте. 🚀
