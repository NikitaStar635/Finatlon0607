# Проектная (учебная) практика

## Участники

| ФИО | Учебная группа | Код направления подготовки | Профиль образовательной программы |
|-|-|-|-|
| Мытницкая Мария Игоревна | 251-339 | 09.03.02 | Автоматизированные системы обработки информации и управления |
| Старостин Никита Андреевич | 251-339 | 09.03.02 | Автоматизированные системы обработки информации и управления |

## Задание

Задание размещено в папке **task** в файле [README.md](task/README.md).

## Вариативная часть задания

Формулировка задания вариативной части и выбранная тематика (если есть). Приведите также дополнительные ссылки на источники задания (если есть).

## Ответственный по проектной (учебной) практике

Меньшикова Наталья Павловна

## Проектная деятельность

Проектная (учебная) практика проводилась в связке с выполнением проекта «***Финатлон. Веб-платформа для финансовых олимпиад***» по дисциплине «Проектная деятельность».

Парамонов Алексей Александрович

## Период проведения

С 03 февраля 2025 г. по 24 мая 2025 г.


## Мини-игра: Змейка

```html
<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Змейка</title>
<style>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: #111;
    margin: 0;
}
canvas {
    background: #222;
    border: 3px solid white;
}
</style>
</head>
<body>

<canvas id="game" width="400" height="400"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

const box = 20;
let snake = [{x: 200, y: 200}];
let food = {
    x: Math.floor(Math.random()*20)*box,
    y: Math.floor(Math.random()*20)*box
};

let direction = "RIGHT";

document.addEventListener("keydown", changeDirection);

function changeDirection(e){
    if(e.key === "ArrowLeft" && direction !== "RIGHT") direction = "LEFT";
    if(e.key === "ArrowUp" && direction !== "DOWN") direction = "UP";
    if(e.key === "ArrowRight" && direction !== "LEFT") direction = "RIGHT";
    if(e.key === "ArrowDown" && direction !== "UP") direction = "DOWN";
}

function draw(){
    ctx.fillStyle = "#222";
    ctx.fillRect(0,0,400,400);

    for(let i=0;i<snake.length;i++){
        ctx.fillStyle = i === 0 ? "lime" : "green";
        ctx.fillRect(snake[i].x, snake[i].y, box, box);
    }

    ctx.fillStyle = "red";
    ctx.fillRect(food.x, food.y, box, box);

    let headX = snake[0].x;
    let headY = snake[0].y;

    if(direction === "LEFT") headX -= box;
    if(direction === "UP") headY -= box;
    if(direction === "RIGHT") headX += box;
    if(direction === "DOWN") headY += box;

    if(headX === food.x && headY === food.y){
        food = {
            x: Math.floor(Math.random()*20)*box,
            y: Math.floor(Math.random()*20)*box
        };
    } else {
        snake.pop();
    }

    const newHead = {x: headX, y: headY};

    if(
        headX < 0 || headY < 0 ||
        headX >= 400 || headY >= 400 ||
        collision(newHead, snake)
    ){
        clearInterval(game);
        alert("Игра окончена!");
    }

    snake.unshift(newHead);
}

function collision(head,array){
    for(let i=0;i<array.length;i++){
        if(head.x === array[i].x && head.y === array[i].y){
            return true;
        }
    }
    return false;
}

let game = setInterval(draw, 120);
</script>

</body>
</html>
