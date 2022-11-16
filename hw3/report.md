## <font size = 5> **HW3 Report** </font>
<p align="right"> 108062119 鄭幃謙 </p>

### <font size=4> **IsFiveInLine()** </font>
```python
def IsFiveInLine(self, x, y):
    player = self.board[x][y]
    count = 1
    for i in range(1, y + 1):
        if self.board[x][y - i] == player:
            count = count + 1
        else:
            break
    for i in range(1, self.size - y):
        if self.board[x][y + i] == player:
            count = count + 1
        else:
            break
    if count >= 5:
        return True
    '''
    other parts
    '''
```
This is how I determine if there are five in a line, which is the part of the vertical line. I check if there are more than five same stones by using `count` to count the numbers of same numbers in a line. The parts of horizonal and diagonal line are the same as this.<br>

### <font size=4> **Bonus** </font>
```python
def cal(board, x, y, size, num, lines, player):
    line = 0
    count = 1
    for i in range(1, y + 1):
        if board[x][y - i] == player:
            count = count + 1
        else:
            break
    for i in range(1, size - y):
        if board[x][y + i] == player:
            count = count + 1
        else:
            break
    if count >= num:
        line += 1
    '''
    other parts
    '''
    return line >= lines

def win(board, x, y, size, player):
    return cal(board, x, y, size, 5, 1, player)

def doubleFour(board, x, y, size, player):
    return cal(board, x, y, size, 4, 2, player)

def four(board, x, y, size, player):
    return cal(board, x, y, size, 4, 1, player)

def doubleThree(board, x, y, size, player):
    return cal(board, x, y, size, 3, 2, player)

def three(board, x, y, size, player):
    return cal(board, x, y, size, 3, 1, player)
```
This is how I determine if there are better moves than the UCT result. `cal()` is similar to the part in `IsFiveInLine()`, but with two more arguments, num and lines, to determine if there are multiple lines of fives, fours or threes. With these functions, I determine the best moves in the order of `win`, `doubleFour`, `four`, `doubleThree` and `three`.<br>


### <font size=4> **Performance** </font>
In the original method, the game usually ends in more than 30 rounds and algorithm often chooses some useless moves, or misses victories. <br>
With the bonus part, the game mostly ends in 20 rounds and never misses victories, which is a great improvement.