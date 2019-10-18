#### 中等难度

#### 描述
- 给定一个 Weather 表，编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 Id

- 给你一个有效的甲板，仅由战舰或者空位组成。
- 战舰只能水平或者垂直放置。换句话说,战舰只能由 1xN (1 行, N 列)组成，或者 Nx1 (N 行, 1 列)组成，其中N可以是任意大小。
- 两艘战舰之间至少有一个水平或垂直的空位分隔 - 即没有相邻的战舰。


- 示例

```shell script
X..X
...X
...X
```
- 在上面的甲板中有2艘战舰

- 无效样例
```shell script
...X
XXXX
...X
```

#### 解答

```shell php
function countBattleships($board) {
    $count = 0;
    $total = count($board);
    for ($i = 0; $i < count($board); $i++) {
        for ($j = 0; $j < count($board[0]); $j++) {
            $isShip = true;
            if ($board[$i][$j] == 'X') {
                $isShip = true;
                if ($i != 0) {
                    if ($board[$i - 1][$j] == 'X') {
                        $isShip = false;
                    }
                }
                if ($j != 0) {
                    if ($board[$i][$j - 1] == 'X') {
                        $isShip = false;
                    }
                }
                if ($isShip) {
                    $count++;
                }
            }
        }
    }
    return  $count;
}

```