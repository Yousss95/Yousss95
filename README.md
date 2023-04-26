import random
def create_snake():
    food = ["O", "O", "O"]
    head = [0, 1]
    body = []
    tail = []
    
    # Create the snake's body and move it towards the food
    for i in range(len(food) - len(body)):
        if (i > 0 and abs(head[0] - food[i]) == 2):
            # Add two segments to the head
            body.append([-1, -1])
            body.append([0, 0])
            
            if head[1]:
                # Rotate upwards
                body[-2][1] += 1
        
        else:
            # Move one segment of the body straight forward
            new_x = head[0] + 1
            new_y = head[1]
            while not (0 <= new_x < len(board) and 0 <= new_y < len(board[0])) or board[new_x][new_y] != "_":
                new_x -= 1
            body.append([new_x, new_y])
    
    return {"position": tuple(reversed(head)), "direction": ("U" if head[1] >= body[0][1] else "D")}

def update_snake(state, key):
    direction = state["direction"]
    position = state["position"]
    
    # Update the snake's movement based on the user input
    if direction == "U":
        next_head = [-1, 0]
    elif direction == "L":
        next_head = [1, 0]
    elif direction == "R":
        next_head = [-1, 1]
    elif direction == "B":
        next_head = [1, 1]
    
    for x in reversed(position[:-1]):
        board[x][position[-1]] = "#"
    
    board[next_head[0]][next_head[1]] = "O"
    state["position"] = next_head + position[-1:]
    return state
