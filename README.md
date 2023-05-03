m = [[1,0,0,0,0,0,0,0,0,1],
     [1,1,1,1,0,0,0,0,0,1],
     [1,0,0,1,1,1,1,1,1,1],
     [1,1,1,1,0,0,0,0,1,0],
     [0,1,0,0,0,0,0,1,1,1],
     [1,1,0,0,0,0,1,1,1,0],
     [0,1,0,1,1,1,1,0,0,0],
     [0,1,0,1,0,0,1,1,1,1],
     [0,1,0,1,0,0,0,1,0,1],
     [1,1,1,1,1,1,1,1,1,1]]

print("Labirintul:")
for x in m:
    print(x)

start = tuple(map(int, input("Start: ").split()))
finish = tuple(map(int, input("Finish: ").split()))

if m[start[0]][start[1]] == 0 or m[finish[0]][finish[1]] == 0:
    print("Start sau Finish invalid!")
    quit()

def get_available_directions(maze, i, j, visited):
    directions = []
    if i + 1 < len(maze) and maze[i+1][j] == 1 and (i+1, j) not in visited:
        directions.append((i+1, j))
    if i > 0 and maze[i-1][j] == 1 and (i-1, j) not in visited:
        directions.append((i-1, j))
    if j + 1 < len(maze[0]) and maze[i][j+1] == 1 and (i, j+1) not in visited:
        directions.append((i, j+1))
    if j > 0 and maze[i][j-1] == 1 and (i, j-1) not in visited:
        directions.append((i, j-1))
    return directions

solutions = []
queue = [(start, [])]
while queue:
    (i, j), visited = queue.pop(0)
    visited.append((i, j))
    if (i, j) == finish:
        solutions.append(visited)
        continue
    directions = get_available_directions(m, i, j, visited)
    if not directions:
        continue
    for direction in directions:
        queue.append((direction, visited[:]))

print(f"\nNumarul de solutii: {len(solutions)}\n")
for i, solution in enumerate(solutions):
    print(f"Solutia nr: {i+1}")
    print(solution)
    for row in range(len(m)):
        for col in range(len(m[0])):
            if (row, col) == start or (row, col) == finish or (row, col) in solution:
                print(" 1 ", end="")
            elif m[row][col] == 0:
                print(" 0 ", end="")
            else:
                print(" - ", end="")
        print()
