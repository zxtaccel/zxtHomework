简易JsPsych实验设计教程：Stroop实验
介绍
本教程将指导您如何使用HTML和JavaScript创建一个简单的Stroop实验。Stroop实验是一种心理学实验，用于研究人们在面对颜色和文字信息冲突时的反应时间。

准备工作
在开始之前，请确保您的计算机上安装了文本编辑器，如Notepad++或Visual Studio Code。

步骤1：创建HTML文件
打开您的文本编辑器。
复制以下HTML代码，并粘贴到新的文本文件中。
html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stroop Experiment</title>
  <style>
    /* CSS样式 */
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      text-align: center;
    }

    .word {
      font-size: 48px;
      margin: 10px;
      padding: 20px;
      border: 1px solid #ccc;
      cursor: pointer;
      user-select: none;
    }
  </style>
</head>

<body>
  <div class="container">
    <div id="stroopWord" class="word" onclick="respond()"></div>
  </div>

  <script>
    // JavaScript代码将在这里编写
  </script>
</body>

</html>
保存文件为stroop_experiment.html。
步骤2：编写JavaScript代码
打开刚才保存的HTML文件。
在<script>标签内，复制并粘贴以下JavaScript代码。
javascript
const colors = ['red', 'green', 'blue', 'yellow'];
const words = ['red', 'green', 'blue', 'yellow'];
let correctResponses = 0;
let totalTrials = 0;

function getRandomColor() {
  return colors[Math.floor(Math.random() * colors.length)];
}

function getRandomWord(isConsistent) {
  let word;
  do {
    word = words[Math.floor(Math.random() * words.length)];
  } while (isConsistent && word !== colors.find(color => color === word));
  return word;
}

function generateStroopWord(isConsistent) {
  const color = getRandomColor();
  const word = getRandomWord(isConsistent);
  const wordElement = document.getElementById('stroopWord');
  wordElement.style.color = color;
  wordElement.textContent = word;
}

function respond() {
  const userResponse = prompt('Please enter the color of the word as described (e.g., red):').toLowerCase();
  const wordElement = document.getElementById('stroopWord');
  const actualWord = wordElement.textContent.toLowerCase();

  // 检查用户的回答是否与字体描述的颜色匹配
  const isCorrect = userResponse === actualWord;

  if (isCorrect) {
    correctResponses++;
    alert(`Correct! You've answered correctly ${correctResponses} times.`);
  } else {
    alert('Wrong, please try again!');
  }

  // 随机决定下一个试次是一致还是不一致
  const nextIsConsistent = Math.random() < 0.5;
  generateStroopWord(nextIsConsistent);
}

document.addEventListener('DOMContentLoaded', () => {
  const initialIsConsistent = Math.random() < 0.5;
  generateStroopWord(initialIsConsistent);
});
步骤3：测试实验
双击stroop_experiment.html文件，它将在您的默认网页浏览器中打开。
点击屏幕上的单词，当弹出提示框时，输入单词描述的颜色。
检查您的回答是否正确，并观察实验如何继续。
步骤4：理解代码
colors和words数组定义了实验中使用的颜色和单词。
getRandomColor和getRandomWord函数用于生成随机颜色和单词。
generateStroopWord函数用于在屏幕上显示Stroop单词。
respond函数处理用户的回答，并提供反馈。
页面加载完成后，第一个Stroop单词将自动生成。
结束语
恭喜您！您已经成功创建了一个简单的Stroop实验。这个实验可以帮助您了解基本的网页编程和心理学实验设计。如果您想进一步学习JsPsych或其他更高级的实验设计工具，请访问它们的官方网站获取更多信息。