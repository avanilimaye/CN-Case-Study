Assignment No. 10 – Group Network Design
and Implementation Case Study

1) Analyze the given requirements and design an appropriate computer network. Implement
and simulate the proposed network using Cisco Packet Tracer.


2) Your solution should demonstrate the application of concepts from the TCP/IP
protocol suite, including IP addressing and subnetting, routing, TCP/UDP
communication, application-layer services, and network-access technologies (as
per your case study).


3) Where appropriate, implement VLANs, DHCP, inter-VLAN communication, Routing protocols,
NAT, DNS, Web/FTP/Email services, wireless connectivity and other such features.


4) The network architecture, IP addressing scheme, VLAN structure, routing approach,
and selection of services should be based on your analysis of the case
requirements.


5) Finally, test the implemented network using appropriate commands and Cisco Packet
Tracer Simulation Mode. Trace selected packets and explain the protocols
involved at different layers of the TCP/IP model.






# Tic-Tac-Toe using Minimax Algorithm

def print_board(board):
    print(board[0] + ' | ' + board[1] + ' | ' + board[2])
    print('---------')
    print(board[3] + ' | ' + board[4] + ' | ' + board[5])
    print('---------')
    print(board[6] + ' | ' + board[7] + ' | ' + board[8])


def check_winner(board):
    winning_positions = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
    ]

    for position in winning_positions:
        a = position[0]
        b = position[1]
        c = position[2]

        if board[a] != ' ' and board[a] == board[b] and board[b] == board[c]:
            return board[a]

    return None


def is_draw(board):#If board is full and no winning combinations
    for cell in board:
        if cell == ' ':
            return False

    return True


def minimax(board, maximizing_player):
    winner = check_winner(board)

    if winner == 'O':
        return 10

    if winner == 'X':
        return -10

    if is_draw(board):
        return 0

    if maximizing_player: #maximizing_player=true =max . look for the largest value
        best_value = -1000

        for i in range(9):
            if board[i] == ' ':
                board[i] = 'O'

                value = minimax(board, False)

                board[i] = ' '

                if value > best_value:
                    best_value = value

        return best_value

    else:
        best_value = 1000

        for i in range(9):
            if board[i] == ' ':
                board[i] = 'X'

                value = minimax(board, True)

                board[i] = ' '

                if value < best_value:
                    best_value = value

        return best_value


def best_move(board):
    best_value = -1000
    move = -1

    for i in range(9):
        if board[i] == ' ':
            board[i] = 'O'

            value = minimax(board, False)

            board[i] = ' '

            if value > best_value:
                best_value = value
                move = i

    return move


board = [' ', ' ', ' ',
         ' ', ' ', ' ',
         ' ', ' ', ' ']

print("TIC-TAC-TOE")
print("You are X")
print("Computer is O")

while True:
    print()
    print_board(board)

    player_move = int(input("Enter your move (0-8): "))

    if player_move < 0 or player_move > 8:
        print("Invalid position")
        continue

    if board[player_move] != ' ':
        print("Position already occupied")
        continue

    board[player_move] = 'X'

    winner = check_winner(board)

    if winner == 'X':
        print_board(board)
        print("You win!")
        break

    if is_draw(board):
        print_board(board)
        print("Draw!")
        break

    computer_move = best_move(board)
    board[computer_move] = 'O'

    winner = check_winner(board)

    if winner == 'O':
        print_board(board)
        print("Computer wins!")
        break

    if is_draw(board):
        print_board(board)
        print("Draw!")
        break
    