import os
import sys
import random

def input_number(message):
	while True:
		try:
			return int(input(message))
		except ValueError:
			print("숫자만 입력하세요.")

def input_bet(money):
	while True:
		bet = input_number("배팅 금액을 입력하세요 : ")
		if bet <= 0:
			print("1원 이상의 금액을 입력하세요.")
		elif bet > money:
			print("현재 잔고보다 많이 배팅할 수 없습니다.")
		else:
			return bet

def ask_again():
	while True:
		again = input("계속 플레이하시겠습니까? (y/n) : ").lower()
		if again == "y":
			return True
		elif again == "n":
			return False
		print("y or n만 입력하세요.")



money = 10000
game_history = []

user_ID = "1"
user_pw = "1"
user_nickname = "BAEK"

while True:
	print("=========================MINI CASINO WORLD==============================")
	print()
	print("1. 로그인")
	print("2. 종료")
	print()
	
	choice = input("선택 : ")
	print()

	if choice == "1":
		print("==========로그인==========")

		input_ID = input("아이디 :")

		print("비밀번호 :", end="", flush=True)

		input_pw = ""

		os.system("stty -icanon -echo")

		while True:
			ch = sys.stdin.read(1)

			if ch == "\r" or ch == "\n":
				break

			input_pw += ch
			print("*", end="", flush=True)

		os.system("stty icanon echo")
		print()

		if input_ID == user_ID and input_pw == user_pw:
			print("로그인 성공!")
			print(user_nickname, "님 환영합니다.")
			print("카지노에 입장합니다.")
			
			while True:
				print()
				print("=========================MINI CASINO WORLD==============================")
				print("현재 잔고 :", money, "원")
				print("1. 슬롯머신")
				print("2. 주사위 게임")
				print("3. 홀짝 게임")
				print("4. 숫자 맞추기")
				print("5. 경마 게임")
				print("6. 카드 게임")
				print("7. 게임 기록")
				print("8. 종료")
				print("==============================")
	
				choice = input("메뉴를 선택하세요 :	")
	
				if choice == "1":
					print()
					print("==============================")
					print("        🎰 슬롯머신 🎰")
					print("==============================")
		
					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money<= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break
						bet = input_bet(money)
						
						money -= bet
		
						num1 = random.randint(1, 9)
						num2 = random.randint(1, 9)
						num3 = random.randint(1, 9)
		
						print()
						print("🎰 결과를 확인합니다...")
						print()
						print("[", num1, "] [", num2, "] [", num3, "]")
						print()
	
						if num1 == num2 == num3:
							reward = bet * 10
							money += reward
	
							print("🎉🎉 JACKPOT!!! 🎉🎉")
							print("배팅금의 10배 당첨!")
							print("당첨금 :", reward, "원")
		
						elif num1 == num2 or num1 == num3 or num2 ==num3:
							reward = bet * 2
							money += reward
	
							print("🎊 2개 일치!")
							print("배팅금의 2배 당첨!")
							print("당첨금 :", reward, "원")
	
						else:
							print("😭 아쉽습니다. 꽝!")
							print("배팅금 :", bet, "원을 잃었습니다.")

						print()
						print("현재 보유 금액 :", money, "원")
						
						if not ask_again():
							print("슬롯머신을 종료합니다.")
							break
								
				elif choice == "2":
					print()
					print("==============================")
					print("        🎲 주사위 게임 🎲")
					print("==============================")

					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money <= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break
						
						bet = input_bet(money)	

						money -= bet

						player_dice = random.randint(1, 6)
						computer_dice = random.randint(1, 6)

						print()
						print("🎲 주사위를 굴립니다...")
						print()
						print("플레이어 :", player_dice)
						print("컴퓨터   :", computer_dice)
						print()

						if player_dice > computer_dice:
							reward = bet * 2
							money += reward

							print("🎉 승리!")
							print("배팅금의 2배를 획득했습니다.")
							print("당첨금 :", reward, "원")

						elif player_dice == computer_dice:
							money += bet

							print("🤝 무승부!")
							print("배팅금을 돌려받았습니다.")
						else:
							print("😭 패배!")
							print("배팅금 :", bet, "원을 잃었습니다.")

						print("현재 보유 금액 :", money, "원")

						if not ask_again():
							print("주사위 게임을 종료합니다.")
							break

				elif choice == "3":
					print("==============================")
					print("        🎯 홀짝 게임 🎯")
					print("==============================")

					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money <= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break

						bet = input_bet(money)
						
						choice_odd_even = input("홀 또는 짝을 선택하세요 (홀/짝) : ")

						if choice_odd_even not in ["홀", "짝"]:
							print("홀 또는 짝만 입력하세요.")
							continue

						money -= bet

						number = random.randint(1, 10)

						if number % 2 == 0:
							result = "짝"
						else:
							result = "홀"

						print()
						print("🎯 숫자를 뽑습니다...")
						print()
						print("나온 숫자 :", number)
						print("결과 :", result)
						print()

						if choice_odd_even == result:
							reward = bet * 2
							money += reward

							print("🎉 정답!")
							print("배팅금의 2배를 획득했습니다.")
							print("당첨금 :", reward, "원")

						else:
							print("😭 틀렸습니다!")
							print("배팅금 :", bet, "원을 잃었습니다.")

						print("현재 보유 금액 :", money, "원")

						if not ask_again():
							print("홀짝 게임을 종료합니다.")
							break

				elif choice == "4":
					print()
					print("==============================")
					print("        🔢 숫자 맞추기 🔢")
					print("==============================")

					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money <= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break

						bet = input_bet(money)

						money -= bet

						answer = random.randint(1, 100)
						count = 0

						print()
						print("1부터 100까지의 숫자 중 하나를 맞혀보세요!")

						while True:
							guess = int(input("숫자를 입력하세요 : "))
							count += 1

							if guess < 1 or guess >100:
								print("1부터 100 사이의 숫자를 입력하세요.")
								continue

							if guess < answer:
								print("⬆️ 더 큰 숫자입니다.")
							elif guess > answer:
								print("⬇️ 더 작은 숫자입니다.")

							else:
								print()
								print("🎉 정답입니다!")
								print("정답 :", answer)
								print("시도 횟수 :", count)

								if count == 1:
									reward = bet * 5
								elif count <=3:
									reward = bet *3
								elif count <=5:
									reward = bet *2
								else:
									reward =bet 

								money += reward

								print("당첨금 :", reward, "원")
								break

						print("현재 보유 금액 :", money, "원")

						if not ask_again():
							print("숫자 맞추기 게임을 종료합니다.")
							break
							
				elif choice == "5":
					print()
					print("==============================")
					print("        🐎 경마 게임 🐎")
					print("==============================")

					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money <= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break

						bet = input_bet(money)


						horse =  input_number("응원할 말을 선택하세요 (1~5) : ")

						if horse < 1 or horse > 5:
							print("1번부터 5번 말 중에서 선택하세요.")
							continue

						money -= bet

						print()
						print("🏇 경마를 시작합니다!")
						print()

						positions = [0, 0, 0, 0, 0]

						while True:
							for i in range(5):
								positions[i] += random.randint(1, 5)

							print("\r", end="")

							for i in range(5):
								print("말", i + 1, ":", "-" * positions[i] + "🐎")

							print()

							winner =None

							for i in range (5):
								if positions[i] >= 30:
									winner = i + 1
									break

							if winner is not None:
								break

						print()
						print("🏆 경주 종료!")
						print("우승마 :", winner, "번 말")
						print()

						if horse == winner:
							reward = bet * 5
							money += reward

							print("🎉 축하합니다! 우승마를 맞혔습니다!")
							print("배팅금의 5배를 획득했습니다.")
							print("당첨금 :", reward, "원")

						else:
							print("😭 아쉽습니다!")
							print("우승마는", winner, "번 말이었습니다.")
							print("배팅금 :", bet, "원을 잃었습니다.")

						print("현재 보유 금액 :", money, "원")

						if not ask_again():
							print("경마 게임을 종료합니다.")
							break
							
				elif choice == "6":
					print()
					print("==============================")
					print("        🃏 카드 게임 🃏")
					print("==============================")

					while True:
						print()
						print("현재 잔고 :", money, "원")

						if money <= 0:
							print("💸 잔고가 모두 소진되었습니다.")
							break

						bet = input_bet(money)

						money -= bet

						player_card = random.randint(1, 13)
						computer_card = random.randint(1, 13)

						print()
						print("🃏 카드를 뽑습니다...")
						print()
						print("플레이어 카드 :", player_card)
						print("컴퓨터 카드 :", computer_card)
						print()

						if player_card > computer_card:
							reward = bet * 2
							money += reward

							print("🎉 승리!")
							print("당첨금 :", reward, "원")

						elif player_card == computer_card:
							money += bet

							print("🤝 무승부!")
							print("배팅금을 돌려받았습니다.")

						else:
							print("😭 패배!")
							print("배팅금 :", bet, "원을 잃었습니다.")

						print("현재 보유 금액 :", money, "원")

						if not ask_again():
							print("카드 게임을 종료합니다.")
							break
							
				elif choice == "7":
					print()
					print("==============================")
					print("        📜 게임 기록 📜")
					print("==============================")

					if len(game_history) == 0:
						print("아직 게임 기록이 없습니다.")

					else:
						for i, record in enumerate(game_history, 1):
							print(i, ".", record)

					print("==============================")
					
				elif choice == "8":
					print("카지노를 종료합니다.")
					break
				else:
					print("잘못된 메뉴입니다.")

		else:
			print("아이디 또는 비밀번호가 틀렸습니다.")
			print("메인 화면으로 돌아갑니다.")

	elif choice == "2":
		print("프로그램을 종료하겠습니다.")
		break
