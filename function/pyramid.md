Pyramid 题总结

目标：
画一个居中、在底部的砖块金字塔。

核心常量：
- BRICK_WIDTH：每块砖的宽
- BRICK_HEIGHT：每块砖的高
- BRICKS_IN_BASE：底层砖的数量
- BRICKS_IN_BASE_X：底层最左边第一块砖的 x 起点

核心思路：
1. 先写一个 draw_bricks(canvas, x, y, color1, color2)
   - 只负责画“单块砖”

2. 再写一个 draw_pyramid(canvas, x, y, color1, color2)
   - 负责画“整个金字塔”

3. 外层循环 row
   - 控制第几层
   - row = 0 是最底层
   - row 越大，层越高，砖越少

4. 每一层的砖数
   - BRICKS_IN_BASE - row

5. 每一层的起点 x
   - start_x = x + row * (BRICK_WIDTH / 2)
   - 因为越往上，每层都要往右缩进半块砖，才能保持居中

6. 每一层的 y
   - start_y = y - (row + 1) * BRICK_HEIGHT
   - 因为画布里 y 越小越往上

7. 内层循环 col
   - 控制这一层的第几块砖
   - brick_x = start_x + col * BRICK_WIDTH

8. 真正画砖时
   - draw_bricks(canvas, brick_x, start_y, color1, color2)

代码骨架：

def main():
    canvas = Canvas(CANVAS_WIDTH, CANVAS_HEIGHT)
    draw_pyramid(canvas, BRICKS_IN_BASE_X, CANVAS_HEIGHT, "red", "yellow")

def draw_pyramid(canvas, x, y, color1, color2):
    for row in range(BRICKS_IN_BASE):
        start_x = x + row * (BRICK_WIDTH / 2)
        start_y = y - (row + 1) * BRICK_HEIGHT

        for col in range(BRICKS_IN_BASE - row):
            brick_x = start_x + col * BRICK_WIDTH
            draw_bricks(canvas, brick_x, start_y, color1, color2)

def draw_bricks(canvas, x, y, color1, color2):
    canvas.create_rectangle(
        x,
        y,
        x + BRICK_WIDTH,
        y + BRICK_HEIGHT,
        color=color1,
        outline=color2
    )

最重要的理解：
- row 管“层”
- col 管“这一层里的砖”
- start_y 让砖一层层往上
- start_x 让每层往右缩进半块砖
- BRICKS_IN_BASE - row 让每层少一块砖

常见错误：
- 在 main 里传了没定义的 y
- 画砖时用了 y 而不是 start_y
- 用 BRICK_WIDTH 去算 start_y
- 函数定义写在 main 里面
- 同时写两套逻辑导致结构乱
