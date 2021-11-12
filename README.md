from random import randint
from sys import exit


# First room
class FirstRoom(object):

    def beginning():
        input("\t\t\tAt the Zoo\n\n\npress enter to play\n")
        print("There is a list of characters you can choose to play")
        print("Each one has a unique utility ability that can be used once per combat")
        print("The utility ability is always the second attack in your choices")
        print("You also regain your max hp at the end of each combat")
        print("Select your character by typing 1, 2 or, 3")
        choice = input("\n1. Tommy the turtle knight\t2. Mitch the texudo monkey\n\n3. Tiffany the toucan magus\n> ")
        if choice == '1':
            character = 'Tommy the turtle knight'

        elif choice == '2':
            character = 'Mitch the texudo monkey'

        elif choice == '3':
            character = 'Tiffany the toucan magus'

        else:
            print("Must type 1, 2 or, 3 only! \nTry again")
            FirstRoom.beginning()

        # intro of game
        print("The sun has long set and it is now midnight")
        print(f"at the georgious zoo known as haaaa and you are {character} and you are")
        print("going to explore it tonight!\n")
        print("You must head to the Entrance, you will need a key in the office however,")
        # for-loops and continue in case player makes a mistake when typing choice
        for yo in character:
            print(f"there are 2 places on the way to the office.\n\nWhere would you like to go first {character}?")
            choice = input("\n\t\t1. Penguin Exhibit\t\t2. Bathroom\n> ")
            # choice 1
            if choice == '1' and character == 'Tommy the turtle knight':
                return SecondRoom.battle_tom()

            elif choice == '1' and character == 'Mitch the texudo monkey':
                return SecondRoom.battle_tex()

            elif choice == '1' and character == 'Tiffany the toucan magus':
                return SecondRoom.battle_tif()

            # choice 2
            elif choice == '2' and character == 'Tommy the turtle knight':
                return SecondRoom.battle_tom2()

            elif choice == '2' and character == 'Mitch the texudo monkey':
                return SecondRoom.battle_tex2()

            elif choice == '2' and character == 'Tiffany the toucan magus':
                return SecondRoom.battle_tif2()

            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue


# 2nd room, depends on character
class SecondRoom(object):
    # choice 1
    def battle_tom():

        confrontation_time_limit = "turns" * 200
        # stats
        penguinHP = 12
        heroHP = 15
        parried = 3
        turn = 0
        stamina = 1
        # intro of battle
        print("As you go through the penguin exhibit you  bump into the emperor and he gets insulted!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. swing\t\t2. parry\t\t3. run away\n> ")
            # player's turn
            if action == '1':
                print("You slash the enemy with your sword!")
                penguinHP -= 3
                print(f"The enemy now has {penguinHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You get in a defensive stance ready for anything")
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("I am sorry, you have zero stamina for this move")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle, 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("On your way out you got a medkit\n\n\n\n")
                    return ThirdRoom.battle_tom3()

                elif chance == 1:
                    print("But you failed")


            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if penguinHP < 0 or penguinHP == 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You got a medkit from that fight\n\n\n\n")
                return ThirdRoom.battle_tom3()


            # if enemy is stunned
            if parried < 3 and parried != 0:
                print("The enemys is still stunned")
                parried -= 1
                continue

            if parried == 0:
                print("The enemy regains his stature!")
                parried += 3

            # enemy's turn
            print("\nThe penguin wobbles at you dangerously!")

            choice = randint(1, 2)

            if choice == 1 and not action == '2':
                print("The penguin pecks you!")
                heroHP -= 3
                print(f"You now have {heroHP} hit points left")

            elif choice == 1 and action == '2':
                print("The penguin comes to peck you however,")
                print("You block his attack stunning him!")
                parried -= 1

            elif choice == 2:
                print("OOPS! He tripped as he wobbled at you")


            # if player hp is down to zero.
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tex():

        confrontation_time_limit = "turns" * 200
        # stats
        penguinHP = 12
        heroHP = 15
        stamina = 1
        turn = 0
        attack = 3
        # intro of battle
        print("As you go through the penguin exhibit you  bump into the emperor and he gets insulted!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. shoot\t\t2. banana\t\t3. run away\n> ")
            # player's turn
            if action == '1':
                print("You shoot the enemy with your gun!")
                penguinHP -= attack
                print(f"The enemy now has {penguinHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You eat a banana, you can feel the potassium coursing throught your veins")
                attack += 2
                heroHP += 4
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("You recieved a medkit on your way out!\n\n\n\n")
                    return ThirdRoom.battle_tex3()

                elif chance == 1:
                    print("But you failed")

            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if penguinHP < 0 or penguinHP == 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You got a medkit from that fight\n\n\n\n")
                return ThirdRoom.battle_tex3()


            # enemy's turn
            print("\nThe penguin wobbles at you dangerously!")

            choice = randint(1, 2)

            if choice == 1:
                print("The penguin pecks you!")
                heroHP -= 3
                print(f"You now have {heroHP} hit points left")

            elif choice == 2:
                print("OOPS! He tripped as he wobbled at you")

            # if player hp is down to zero
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tif():

        confrontation_time_limit = "turns" * 200
        #stats
        penguinHP = 12
        heroHP = 15
        stamina = 1
        turn = 0
        # the variable below is used to get an if-statements working
        polymorph = 2
        # intro of battle
        print("As you go through the penguin exhibit you  bump into the emperor and he gets insulted!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. blast\t\t2. polymorph\t\t3. run away\n> ")
            # player's turn
            if action == '1':
                print("You blast the enemy with your magic!")
                penguinHP -= 3
                print(f"The enemy now has {penguinHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You polymorph the enemy, a cloud of smoke is before you")
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("You recieved a medkit on your way out!\n\n\n\n")
                    return ThirdRoom.battle_tif3()

                elif chance == 1:
                    print("But you failed")


            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if penguinHP == 0 or penguinHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You got a medkit from that fight\n\n\n\n")
                return ThirdRoom.battle_tif3()


            # if enemy is polymorphed on his turn
            if action == '2':
                # for fun the enemy can polymorph into 3 different things
                polly = randint(1, 3)

                if polly == 1:
                    polly = 'ballooon'

                elif polly == 2:
                    polly = 'party hat'

                elif polly == 3:
                    polly = 'birthday cake'

                print(f"The smoke clears, enemy is now a {polly}")
                decision = randint(1, 2)
                # when enemy is polymorphed on his turn he can either fight or resist curse
                if decision == 1:

                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)
                    # enemy only has 10% of turning back to normal
                    if attempt == 1:
                        print("He succeeded!")
                        penguinHP = 12
                        pass

                    else:
                        print("He failed and can do nothing")
                        penguinHP = 6
                        continue

                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    penguinHP = 6
                    polymorph = 1
                    continue


            if polymorph == 1:
                print(f"The enemy is now a {polly}")
                decision = randint(1, 2)

                if decision == 1:
                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)

                    if attempt == 1:
                        print("He succeeded!")
                        polymorph = 2
                        penguinHP = 12
                        pass

                    else:
                        print("He failed and can do nothing")
                        penguinHP = 3
                        polymorph = 1
                        continue
                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    penguinHP = 3
                    polymorph = 1
                    continue


            # enemy's turn
            print("\nThe penguin wobbles at you dangerously!")

            choice = randint(1, 2)

            if choice == 1:
                print("The penguin pecks you!")
                heroHP -= 3
                print(f"You now have {heroHP} hit points left")

            elif choice == 2:
                print("OOPS! He tripped as he wobbled at you")


            # if player hp is down to zero or if fight lasts too long if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    #choice 2
    def battle_tom2():

        confrontation_time_limit = "turns" * 200
        # stats
        toiletHP = 12
        heroHP = 15
        parried = 3
        turn = 0
        stamina = 1
        # this variable is here to make an if statement work
        choice = 1
        # intro of battle
        print("OK, for some reason out of of all those epic choices you chose the bathroom. You walk into the restroom and water")
        print("is all over the floor. A stall opens and a pissed off toilet walks through it mouth watering for your blood!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. swing\t\t2. parry\t\t3. run away\n> ")
            # player's turn
            if action == '1':
                print("You slash the enemy with your sword!")
                toiletHP -= 3
                print(f"The enemy now has {toiletHP} hit points left")

            elif action == '2' and choice != 2 and stamina == 1:
                print("You get in a defensive stance ready for anything")
                stamina -= 1

            elif action == '2' and choice == 2 and stamina == 1:
                print("You try to get in a defensive stance however, the new water that the toilet")
                print("has overflowed over you seems to have canceled it's power")
                stamina -= 1
                parried += 1

            elif action == '2' and stamina == 0:
                print("I am sorry, you have zero stamina for this move")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("And on your way you found a medkit!\n\n\n\n")
                    return ThirdRoom.battle_tom3()

                elif chance == 1:
                    print("But you failed")


            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if toiletHP == 0 or toiletHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You recieved a medkit from the enemy!\n\n\n\n")
                return ThirdRoom.battle_tom3()


            # if enemy is stunned
            if parried < 3 and parried != 0:
                print("The enemys is still stunned")
                parried -= 1
                continue

            if parried == 0:
                print("The enemy regains his stature!")
                parried += 3

            # enemy's turn
            print("\nThe toilet approaches you rudely!")

            choice = randint(1, 2)

            if choice == 1 and not action == '2':
                print("The toilet flushes!")
                heroHP -= 3
                print(f"You now have {heroHP} hit points left")

            elif choice == 1 and action == '2' and parried == 3:
                print("The toilet tries to flush on you however,")
                print("You block its attack stunning the enemy!")
                parried -= 1
            # this enemy has an abilty that cancels your utility ability if used last turn
            elif choice == 2 and not action == '2':
                print("The toilet overflows!")

            elif choice == 2 and action == '2' and parried == 3:
                print("The toilet tries to overflow however,")
                print("You block its attack stunning the enemy!")
                parried -= 1


            # if player hp is down to zero or if fight lasts too long if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tex2():

        confrontation_time_limit = "turns" * 200
        # stats
        toiletHP = 12
        heroHP = 15
        turn = 0
        stamina = 1
        attack = 3
        # this variable is here to make an if statement work
        choice = 1
        # Intro of battle
        print("OK, for some reason out of of all those epic choices you chose the bathroom. You walk into the restroom and water")
        print("is all over the floor. A stall opens and a pissed off toilet walks through it mouth watering for your blood!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            # player's turn
            action = input("\n\n\t\t1. shoot\t\t2. banana\t\t3. run away\n> ")

            if action == '1':
                print("You shoot the enemy with your gun!")
                toiletHP -= attack
                print(f"The enemy now has {toiletHP} hit points left")

            elif action == '2' and choice != 2 and stamina == 1:
                print("You eat a banana you can feel the potassium coursing through your veins!")
                heroHP += 4
                attack += 2
                stamina -= 1

            elif action == '2' and choice == 2 and stamina == 1:
                print("You eat your banana however, the new water that the toilet")
                print("has overflowed over you seems to have canceled it's power")
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle, 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("You recieved a medkit on your way out!\n\n\n\n")
                    return ThirdRoom.battle_tex3()

                elif chance == 1:
                    print("But you failed")


            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if toiletHP == 0 or toiletHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You recieved a medkit from the enemy!\n\n\n\n")
                return ThirdRoom.battle_tex3()


            # enemy's turn
            print("\nThe toilet approaches you rudely!")

            choice = randint(1, 2)

            if choice == 1:
                print("The toilet flushes!")
                heroHP -= 1
                print(f"You now have {heroHP} hit points left")
            # this enemy has an abilty that cancels your utility ability if used last turn
            elif choice == 2:
                print("The toilet overflows!")

            # if player hp is down to zero
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tif2():

        confrontation_time_limit = "turns" * 200
        # stats
        toiletHP = 12
        heroHP = 15
        turn = 0
        stamina = 1
        # the 3 variables below are to get some if-statements working
        polymorph = 2
        choice = 1
        work = 0
        # intro of battle
        print("OK, for some reason out of of all those epic choices you chose the bathroom. You walk into the restroom and water")
        print("is all over the floor. A stall opens and a pissed off toilet walks through it mouth watering for your blood!")
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. blast\t\t2. polymorph\t\t3. run away\n> ")
            # player's turn
            if action == '1':
                print("You blast the enemy with your magic!")
                toiletHP -= 3
                print(f"The enemy now has {toiletHP} hit points left")

            elif action == '2' and choice != 2 and stamina == 1:
                print("You polymorph the enemy, a cloud of smoke is before you")
                stamina -= 1

            elif action == '2' and choice == 2 and stamina == 1:
                print("You attempt to polymorph the enemy however,")
                print("the new water that the toilet has")
                print("overflowed over you seems to have canceled it's power")
                stamina -= 1
                work += 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue

            elif action == '3':
                print("You attempt to run....")
                chance = randint(1, 4)
                # mechanic to avoid battle 75% success
                if chance > 1 and chance != 1:
                    print("Success, You escape")
                    input("You recieved a medkit on your way out!\n\n\n\n")
                    return ThirdRoom.battle_tif3()

                elif chance == 1:
                    print("But you fail")


            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if toiletHP == 0 or toiletHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You recieved a medkit from the enemy!\n\n\n\n")
                return ThirdRoom.battle_tif3()



            # if enemy is polymorphed on his turn
            if action == '2' and work != 1:
                polly = randint(1, 3)
                # for fun the enemy can polymorph into 3 different things
                if polly == 1:
                    polly = 'ballooon'

                elif polly == 2:
                    polly = 'party hat'

                elif polly == 3:
                    polly = 'birthday cake'

                print(f"The smoke clears, enemy is now a {polly}")
                decision = randint(1, 2)

                if decision == 1:

                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)
                    # 10% he succeeds
                    if attempt == 1:
                        print("He succeeded!")
                        toiletHP = 12
                        pass

                    else:
                        print("He failed and can do nothing")
                        toiletHP = 6
                        polymorph = 1
                        continue

                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    toiletHP = 6
                    polymorph = 1
                    continue


            if polymorph == 1:
                print(f"The enemy is now a {polly}")
                decision = randint(1, 2)

                if decision == 1:
                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)

                    if attempt == 1:
                        print("He succeeded!")
                        polymorph = 2
                        toiletHP = 12
                        pass

                    else:
                        print("He failed and can do nothing")
                        toiletHP = 3
                        polymorph = 1
                        continue

                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    toiletHP = 3
                    polymorph = 1
                    continue


            # enemy's turn
            print("\nThe toilet approaches you rudely!")

            choice = randint(1, 2)

            if choice == 1:
                print("The toilet flushes!")
                heroHP -= 1
                print(f"You now have {heroHP} hit points left")
            # this enemy has an abilty that cancels your utility ability if used last turn
            elif choice == 2:
                print("The toilet overflows!")


            # if player hp is down to zero or if fight lasts too long if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")


# 3rd room, depends on character
class ThirdRoom(object):

    def battle_tom3():

        confrontation_time_limit = "turns" * 200
        #stats
        janitorHP = 15
        heroHP = 15
        parried = 3
        turn = 0
        stamina = 1
        medkit = 1
        # battle intro
        print("You head into the office of the zoo and find the keys hanging on the wall. You try to reach")
        print("for them however, you are just a cute short little animal. A human hand reaches over and grabs them")
        print("You turn around to see the janitor jingling the keys in a sinister way in front of you")
        print('\njanitor-"Looking for these? >=D"')
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. swing\t\t2. parry\t\t3. medkit\n> ")
            # player's turn
            if action == '1':
                print("You slash the enemy with your sword!")
                janitorHP -= 3
                print(f"The enemy now has {janitorHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You get in a defensive stance ready for anything")
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("I am sorry, you have zero stamina for this move")
                continue
            # medkit heals 12 hp, your max hp is 15
            elif action == '3' and heroHP == 3 or heroHP > 3 and medkit == 1:
                print("You use up your medkit")
                heroHP = 15
                print("Your hitpoints max out")
                medkit -= 1

            elif action == '3' and heroHP < 3 and medkit == 1:
                print("You use up your medkit")
                heroHP += 12
                print(f"You now have {heroHP} hit points")
                medkit -= 1

            elif action == '3' and medkit == 0:
                print("You already used up your medkit")
                continue

            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if janitorHP == 0 or janitorHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You got gate keys from that fight\n\n\n\n")
                return LastRoom.Entrance()


            # if enemy is stunned
            if parried < 3 and parried != 0:
                print("The enemys is still stunned")
                parried -= 1
                continue

            if parried == 0:
                print("The enemy regains his stature!")
                parried += 3

            # enemy's turn
            print("\nThe janitor mops your way!")

            choice = randint(1, 10)

            if choice != 10 and not action == '2':
                print("YOU JUST GOT MOPPED!")
                heroHP -= 4
                print(f"You now have {heroHP} hit points left")

            elif choice != 10 and action == '2':
                print("The janitor tries to mop on you however,")
                print("You block its attack stunning the enemy!")
                parried -= 1
            # enemy has 10% of healing on his turn
            elif choice == 10 and janitorHP < 8 or janitorHP == 8:
                print("The janitor washes his hands!")
                janitorHP += 6
                print(f"The enemy now has {janitorHP} hp left")

            elif choice == 10 and janitorHP > 8:
                print("The janitor washes his hands!")
                janitorHP = 15
                print("The enemy's hp is maxed out!")


            # if player hp is down to zero or if fight lasts too long if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tex3():

        confrontation_time_limit = "turns" * 200
        # stats
        janitorHP = 15
        heroHP = 15
        stamina = 1
        attack = 3
        medkit = 1
        turn = 0
        # Intro of battle
        print("You head into the office of the zoo and find the keys hanging on the wall. You try to reach")
        print("for them however, you are just a cute short little animal. A human hand reaches over and grabs them")
        print("You turn around to see the janitor jingling the keys in a sinister way in front of you")
        print('janitor-"Looking for these? >=D"')
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")
            # player's turn
            action = input("\n\n\t\t1. shoot\t\t2. banana\t\t3. medkit\n> ")

            if action == '1':
                print("You shoot the enemy with your gun!")
                janitorHP -= attack
                print(f"The enemy now has {janitorHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You eat a banana, you can feel the potassium coursing throught your veins")
                attack += 2
                heroHP += 4
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue
            # medkit heals 12 hp, your max hp is 15
            elif action == '3' and heroHP == 3 or heroHP > 3 and medkit == 1:
                print("You use up your medkit")
                heroHP = 15
                print("Your hitpoint max out")
                medkit -= 1

            elif action == '3' and heroHP < 3 and medkit == 1:
                print("You use up your medkit")
                heroHP += 12
                print(f"Yoi now have {heroHP} hit points")
                medkit -= 1

            elif medkit == 0 and action == '3':
                print("You already used up your medkit")
                continue

            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if janitorHP == 0 or janitorHP < 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                input("You got gate keys from that fight\n\n\n\n")
                return LastRoom.Entrance()


            # enemy's turn
            print("\nThe janitor mops your way!")

            choice = randint(1, 10)

            if choice != 10:
                print("YOU JUST GOT MOPPED!")
                heroHP -= 4
                print(f"You now have {heroHP} hit points left")
            # enemy has 10% of healing on his turn
            elif choice == 10 and janitorHP < 8 or janitorHP == 8:
                print("The janitor washes his hands!")
                janitorHP += 6
                print(f"The enemy now has {janitorHP} hp left")

            elif choice == 10 and janitorHP > 8:
                print("The janitor washes his hands!")
                janitorHP = 15
                print("The enemy's hp is maxed out!")
                print(janitorHP)

            # if player hp is down to zero or if fight lasts too long if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")

    def battle_tif3():

        confrontation_time_limit = "turns" * 200
        # stats
        janitorHP = 15
        heroHP = 15
        turn = 0
        stamina = 1
        medkit = 1
        # the variable below is for getting an if-statements working
        polymorph = 2
        # intro of battle
        print("You head into the office of the zoo and find the keys hanging on the wall. You try to reach")
        print("for them however, you are just a cute short little animal. A human hand reaches over and grabs them")
        print("You turn around to see the janitor jingling the keys in a sinister way in front of you")
        print('janitor-"Looking for these? >=D"')
        print("\n\t\t\t*Fight begins*")
        for yo in confrontation_time_limit:

            turn += 1
            print(f"Turn {turn}")

            action = input("\n\n\t\t1. blast\t\t2. polymorph\t\t3. medkit\n> ")
            # player's turn
            if action == '1':
                print("You blast the enemy with your magic!")
                janitorHP -= 3
                print(f"The enemy now has {janitorHP} hit points left")

            elif action == '2' and stamina == 1:
                print("You polymorph the enemy, a cloud of smoke is before you")
                stamina -= 1

            elif action == '2' and stamina == 0:
                print("You dont have enough stamina for this")
                continue
            # medkit heals 12 hp, your max hp is 15
            elif action == '3' and heroHP == 4 or heroHP > 4 and medkit == 1:
                print("You use up your medkit")
                heroHP = 12
                print("Your hitpoint max out")
                medkit -= 1

            elif action == '3' and heroHP < 4 and medkit == 1:
                print("You use up your medkit")
                heroHP += 8
                print(f"Yoi now have {heroHP} hit points")
                medkit -= 1

            elif medkit == 0:
                print("You already used up your medkit")
                continue

            else:
                print("Must type 1, 2 or, 3 only! \nTry again")
                continue

            if janitorHP < 0 or janitorHP == 0:
                print("\n\t\t\t*victory music*\nCongrats you won!")
                return LastRoom.Entrance()


            # if enemy is polymorphed on his turn
            if action == '2':
                polly = randint(1, 3)
                # for fun the enemy can polymorph into 3 different things
                if polly == 1:
                    polly = 'ballooon'

                elif polly == 2:
                    polly = 'party hat'

                elif polly == 3:
                    polly = 'birthday cake'

                print(f"The smoke clears, enemy is now a {polly}")
                decision = randint(1, 2)

                if decision == 1:

                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)
                    # 10% he succeeds
                    if attempt == 1:
                        print("He succeeded!")
                        janitorHP = 15
                        pass

                    else:
                        print("He failed and can do nothing")
                        janitorHP = 6
                        polymorph = 1
                        continue

                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    janitorHP = 6
                    polymorph = 1
                    continue


            if polymorph == 1:
                print(f"The enemy is now a {polly}")
                decision = randint(1, 2)

                if decision == 1:
                    print("He tries to resist his curse....")
                    attempt = randint(1, 10)

                    if attempt == 1:
                        print("He succeeded!")
                        polymorph = 2
                        janitorHP = 15
                        pass

                    else:
                        print("He failed and can do nothing")
                        janitorHP = 3
                        polymorph = 1
                        continue

                elif decision == 2:
                    print(f"The now {polly} hops over to you!")
                    heroHP -= 1
                    print(f"You now have {heroHP} hit points left")
                    janitorHP = 3
                    polymorph = 1
                    continue


            # enemy's turn
            print("\nThe janitor mops your way!")

            choice = randint(1, 10)

            if choice != 10:
                print("YOU JUST GOT MOPPED!")
                heroHP -= 4
                print(f"You now have {heroHP} hit points left")
            # enemy has 10% of healing on his turn
            elif choice == 10 and janitorHP < 8 or janitorHP == 8:
                print("The janitor washes his hands!")
                janitorHP += 6
                print(f"The enemy now has {janitorHP} hp left")

            elif choice == 10 and janitorHP > 8:
                print("The janitor washes his hands!")
                janitorHP = 15
                print("The enemy's hp is maxed out!")


            # if player hp is down to zero, if not continue fight
            if heroHP == 0 or heroHP < 0:
                print("\n*ZLOPP*\nYou have been DEFEATED")
                exit()

            else:
                print("\nThe fight continues\n")


# Last room
class LastRoom(object):
    # unlock gate with key, face the boss, win game!
    def Entrance():
        print("You use the key to open the gate to the main entrance and step out of the zoo")
        print('"HOLD IT RIGHT THERE!"')
        print("You stop were you stand.... \nHero-'Who is out there?'")
        print('"IT IS I HAAAA THE ZOO AND YOU MUST ANSWER MY RIDDLE IF YOU WANT TO LEAVE!"')
        print("You turn around to see the zoo talking to you")
        print('Hero-"What do you want from me?"')
        input('Haaa-"YOU MUST ANSWER MY RIDDLE CORRECTLY OR DIE!!!"\n> ')

        print("\nOnce upon a time there was a slime monster that grows a limb when hit,")
        print("loses one when making fun of it and, multiplies by 6.25 when you dance")
        print("How many limbs would it have if it started with no limbs and in this order you")
        print("Make fun of it twice in a row, hit it 3 times in a row, and then danced twice in a row?")
        print("When you have your answer round it off to the nearest hundredths place and write your answer in scientific notation")
        input('\nHero-"Its 1.1719 x 10^2 you idiot! git gud scrub"\n> ')


        print('\nHaaa-"NOOOOOOO YOU HAVE DEFEATED ME AND ON MY OWN BIRTHDAY NOOOOOOOO!"')
        print("*victory music*")

        print("\nYou step outside the zoo to visit your favorite ice cream shop as you do every year and order an ice cream sundae")
        print("\t\t\tThe End.")

        print("\n\nThank you for playing!\nI hope you enjoyed this from an amateur programmer")
        print("will appreciate any tips or advice whether in the actual code or gameplay to help improve myself for the near future")
        exit()


# starts game
FirstRoom.beginning()
