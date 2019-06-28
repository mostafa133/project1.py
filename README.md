# project1.py
player1 = "X"
player2 = "O"

def print_board(table):
    for i in range(len(table)):
        for j in range(len(table[i])):
            print table[i][j],
        print("")

def main():
    table = [["_", "_", "_"],["_", "_", "_"],["_", "_", "_"]]
    turn = player1
    counter = 0

    while True:
        print_board(table)
        print "Next turn:", turn
        row = int(input("press enter row: "))
        col = int(input("press enter col: "))
        while not validInput(row, col,table):
            print("input is invalid, please try again:")
            row = int(input("press enter row: "))
            col = int(input("press enter col: "))
        counter = counter + 1
        table[row][col] = turn

        if isWinner(row,col, table, turn):
            print("{0} is the winner".format(turn))
            print_board(table)
            break

        if gameOver(table , counter):
            print("tiko")
            print_board(table)
            break


        turn = changeTurn(turn)

def validInput (row , col , table):
    if col < 0 or col > 2 or row > 2 or row < 0:
        return False
    if table[row][col] == "_":
        return True
    return False

def gameOver(table, counter):
    if counter == 9 :
        return True
    else:
        return False

def changeTurn(turn):
    if turn == player1:
        return player2
    elif turn == player2:
        return player1

def isWinner (row, col, table, turn):

    # check row
    for i in range(3):
        if table[row][i] != turn:
            break
    else:
        return True

    # check col
    for i in range(3):
        if table[i][col]  != turn:
            break
    else:
        return True

    if (row!=1 and col==1) or  (row==1 and col!=1) :
        return False

    if ((table[0][0] == turn and table[1][1] == turn and table[2][2] == turn)
        or (table[0][2]== turn and table[1][1]==turn and table[2][0]==turn)):
        return True

    return False

main()
