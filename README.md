# python3project

#Fun_With_Cards


import random

diamond_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
user_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
computer_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
player1_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
player2_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
player3_cards = [2,3,4,5,6,7,8,9,10,11,12,13,14]
player1_score = []
player2_score = []
player3_score = []
comp_score=[]
user_score=[]
sc1,sc2,sc3=0,0,0

def diamond_generator():
    p = random.choice( diamond_cards)
    return p
       
def user_generator():
    n = int(input())
    if n in user_cards:
        user_cards.remove(n)
    else:
        print("Choose the cards from the list ")
        user_generator()
    return n

def top_five():
  if len( diamond_cards) >= 5:
    top_list =  diamond_cards[len( diamond_cards)-5:len( diamond_cards)]
  else:
    top_list =  diamond_cards
  return top_list

def computer_choice(bid_value):
    computer_options = []
    max = top_five()
   # print("max = ",max)
    if bid_value in max:
        for card in computer_cards:
            if bid_value <= card:
                computer_options.append(card)
       # print("options = ",computer_options)
        if len(computer_options) > 1:
            res = computer_options[1]
        elif len(computer_options) == 1:
            res = computer_options[0]
        elif len(computer_options) == 0:
            res = computer_cards[-1]
    else:
        for card in computer_cards:
            if bid_value >= card:
                computer_options.append(card)
      #  print("options = ",computer_options)
        if len(computer_options) > 1:
            res = computer_options[-2]

        elif len(computer_options) == 1:
            res = computer_options[0]
        elif len(computer_options) == 0:
            res = computer_cards[-1]
    computer_cards.remove(res)
    diamond_cards.remove(bid_value)
    return res

def bidding_score1(user,comp,d):
    if user > comp:
        user_score.append(d)
        print("You won the Bidding ")
         
    elif user == comp:
          user_score.append(d/2)
          comp_score.append(d/2)
          print("Both have Bidded the same value ")
    else:
        comp_score.append(d)
        print("You have lost the bidding ")
    sc1 = sum(user_score)
    sc2 = sum(comp_score)  
    return sum(user_score),sum(comp_score)


def bidding1():
    for i in range(0,13):
        bid_value=diamond_generator()
        #print(computer_cards)
        print("bid_value ", bid_value)
        print("Your cards ",user_cards)
        computers_choice = computer_choice(bid_value)
        user_choice=user_generator()
        print("Comp",computers_choice,user_choice)
        sc1, sc2 = bidding_score1(user_choice, computers_choice, bid_value)
    print("User score , computer score",sc1, sc2)
    if sc1 > sc2:
        return 1;
    elif sc1 == sc2:
        return -1;
    else:
        return 0;
       
def player1_generator():
    while True:
        n=int(input())
        if n in player1_cards:
            player1_cards.remove(n)
            break
        print("choose from the list")
    return n

def player2_generator():
    while True:
        n=int(input())
        if n in player2_cards:
            player2_cards.remove(n)
            break
        print("choose from the list")
    return n

def player3_generator():
    while True:
        n=int(input())
        if n in player3_cards:
            player3_cards.remove(n)
            break
        print("choose from the list")
    return n



def bidding_score3(player1,player2,player3,d):
    high = max(player1, player2, player3)
    if player1 == high and player2 == high and player3 == high:
        player1_score.append(d / 3)
        player2_score.append(d / 3)
        player3_score.append(d / 3)
        print("All have bidded the same value")        
    elif player1 == high and player2 == high:
          player1_score.append(d / 2)
          player2_score.append(d / 2)
          print("Player1 and Player2 have Bidded the same value ")
    elif player1 == high and player3 == high:
          player1_score.append(d / 2)
          player3_score.append(d / 2)
          print("Player1 and Player3 have Bidded the same value ")
    elif player2 == high and player3 == high:
          player2_score.append(d / 2)
          player3_score.append(d / 2)
          print("Player2 and Player3 have Bidded the same value ")
    elif player1 == high:
          player1_score.append(d)
          print("Player1 won the bidding")
    elif player2 == high:
          player2_score.append(d)
          print("Player2 won the bidding")
    else:
          player3_score.append(d)
          print("Player3 won the bidding")
    sc1 = sum(player1_score)
    sc2 = sum(player2_score)
    sc3 = sum(player3_score)
    return sum(player1_score),sum(player2_score),sum(player3_score)


def bidding3():
    for i in range(0,13):
        bid_value=diamond_generator()
        diamond_cards.remove(bid_value)
        #print(computer_cards)
        print("bid_value ", bid_value)
        print("Diamond cards ", diamond_cards)
        print("Player1 cards ",player1_cards)
        print("Player2 cards ",player2_cards)
        print("Player3 cards ",player3_cards)
        player1_choice = player1_generator()
        player2_choice = player2_generator()
        player3_choice = player3_generator()
        print("Comp",player1_choice,player2_choice,player3_choice)
        sc1, sc2, sc3 = bidding_score3(player1_choice, player2_choice, player3_choice, bid_value)
    print("player1 score , player2 score, player3 score ",sc1, sc2, sc3)
    if sc1 == sc2 and sc2 == sc3:
        return 1, 1, 1;
    elif sc1 > sc2 and sc1 > sc3:
        return 1, 0, 0
    elif sc2 > sc1 and sc2 > sc3:
        return 0, 1, 0;
    elif sc3 > sc1 and sc3 > sc2:
        return 0, 0, 1;
    elif sc1 == sc2 and sc2 > sc3:
        return 1, 1, 0;
    elif sc2 == sc3 and sc2 > sc1:
        return 0, 1, 1;
    else:
        return 1, 0, 1;
   


def bidding_score2(player1,player2,d):
    if player1 > player2:
        player1_score.append(d)
        print("PLAYER1 won the Bidding ")
         
    elif player1 == player2:
          player1_score.append(d/2)
          player2_score.append(d/2)
          print("Both have Bidded the same value ")
    else:
        player2_score.append(d)
        print("PLAYER2 the bidding ")
    sc1 = sum(player1_score)
    sc2 = sum(player2_score)  
    return sum(player1_score),sum(player2_score)

def bidding2():
    for i in range(0,13):
        bid_value=diamond_generator()
        diamond_cards.remove(bid_value)
        #print(computer_cards)
        print("bid_value ", bid_value)
        print("Diamond cards ", diamond_cards)
        print("Player1 cards ",player1_cards)
        print("Player2 cards ",player2_cards)
        player1_choice = player1_generator()
        player2_choice = player2_generator()
        print("Comp",player1_choice,player2_choice)
        sc1, sc2 = bidding_score2(player1_choice, player2_choice, bid_value)
    print("player1 score , player2 score ",sc1, sc2)
    if sc1 == sc2:
        return 1, 1;
    elif sc1 > sc2:
        return 1, 0;
    else:
        return 0, 1;
   

print("SINGLE PLAYER : 1")
print("TWO PLAYERS   : 2")
print("THREE PLAYERS : 3")
n = int(input())
if n == 1:
    print("ENTER YOUR NAME : ")
    name = input()
    score = bidding1()
    if score == 1:
        print(name, "WON THE GAME")
    elif score == -1:
        print("TIE MATCH")
    else:
        print("COMPUTER WON THE GAME")
elif n == 2:
    print("ENTER PLAYER1 NAME : ")
    name1 = input()
    print("ENTER PLAYER2 NAME : ")
    name2 = input()
    score1, score2 = bidding2()
    if score1 == 1 and score2 == 1:
        print("TIE BETWEEN ", name1, "and ", name2)
    elif score1 == 1:
        print(name1," WON THE GAME")
    else:
        print(name2," WON THE GAME")
else:
    print("ENTER PLAYER1 NAME : ")
    name1 = input()
    print("ENTER PLAYER2 NAME : ")
    name2 = input()
    print("ENTER PLAYER3 NAME : ")
    name3 = input()
    score1, score2, score3 = bidding3()
    if score1 == score2 and score2 == score3:
        print("MATCH TIED BETWEEN THE THREE PLAYERS")
    elif score1 > score2 and score1 > score3:
        print(name1," WON THE GAME")
    elif score2 > score1 and score2 > score3:
        print(name2," WON THE GAME")
    elif score3 > score1 and score3 > score2:
        print(name3," WON THE GAME")
    elif score1 == score2 and score2 > score3:
        print("TIE BETWEEN ",name1," AND ",name2)
    elif sc2 == sc3 and sc2 > sc1:
        print("TIE BETWEEN ",name2," AND ",name3)
    else:
        print("TIE BETWEEN ",name1," AND ",name3)
