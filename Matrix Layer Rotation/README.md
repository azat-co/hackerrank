Your Matrix Layer Rotation submission got 62.22 points.

Test Case #4 and Test Case #5 are failing out of 12.

[Input for Test Case #5](https://hr-testcases-us-east-1.s3.amazonaws.com/8965/input05.txt?AWSAccessKeyId=AKIAJ4WZFDFQTZRGO3QA&Expires=1501612357&Signature=i15Yw0%2BpoH67w0lbgYV%2BusyKkG4%3D&response-content-type=text%2Fplain)

[Input for Test Case #4](https://hr-testcases-us-east-1.s3.amazonaws.com/8965/input04.txt?AWSAccessKeyId=AKIAJ4WZFDFQTZRGO3QA&Expires=1501612821&Signature=2LuG%2BNorKrSQgczmAyqTxAkHivs%3D&response-content-type=text%2Fplain)

```js
function processData(input) {
    //Enter your code here
  let lines = input.split('\n')
  let m = lines[0].split(' ')[0]
  let n = lines[0].split(' ')[1]
  let r = parseInt(lines[0].split(' ')[2], 10)
  //console.log(m, n, r)
  lines.splice(0,1)
  let matrix = lines.map((line)=>{return line.split(' ')})
  //console.log(matrix)
     let snakes = []
  if (m<=n) {
    maxSnakes = Math.floor(m/2)
  } else {
    maxSnakes = Math.floor(n/2)
  }
  for (let si=0; si<maxSnakes; si++) {
    let snake = []
    for (let i=si; i<n-si; i++) {
      snake.push(matrix[si][i])
    }
    for (let j=si+1; j<m-si-1; j++) {
      snake.push(matrix[j][n-si-1])
    }
      
    for (let i=n-si-1; i>=si; i--) {
      snake.push(matrix[m-si-1][i])
    }
    for (let j=m-si-2; j>si; j--) {
      snake.push(matrix[j][si])
    }          
    snakes.push(snake)
  }

//  console.log(snakes)

  snakes = snakes.map((snake, index, list)=>{
    if (r>=snake.length) {
      rSnake = r % snake.length
    } else {
      rSnake = r
    }

    snake = snake.map((item, i, list)=>{
      let newI = i + rSnake
      if (newI>list.length-1) 
        newI = newI % list.length
      return list[newI]
    })
//    for (let ri = 0; ri<r; ri++) {  
//      let first = snake.shift()
//      snake.push(first)
//    }
   // console.log(first, snake)
    return snake
  })
  // console.log(snakes)

  for (let si=0; si<maxSnakes; si++) {
    let snake = snakes.shift()
    for (let i=si; i<n-si; i++) {
      matrix[si][i]=snake.shift()
    }
    for (let j=si+1; j<m-si-1; j++) {
      matrix[j][n-si-1] = snake.shift()
    }
      
    for (let i=n-si-1; i>=si; i--) {
      matrix[m-si-1][i] = snake.shift()
    }
    for (let j=m-si-2; j>si; j--) {
      matrix[j][si] = snake.shift()
    }          

  }
  matrix.forEach((line)=>console.log(line.join(' ')))
} 

process.stdin.resume();
process.stdin.setEncoding("ascii");
_input = "";
process.stdin.on("data", function (input) {
    _input += input;
});

process.stdin.on("end", function () {
   processData(_input);
});

```