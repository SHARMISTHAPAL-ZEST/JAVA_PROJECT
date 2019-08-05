# JAVA_PROJECT
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.InputMismatchException;
import java.util.Random;
import java.util.Scanner;

public class TicTacToe {

	static char boardArray[][] = { { '1', '2', '3' }, { '4', '5', '6' }, { '7', '8', '9' } };
	static char var1, var2;
	static boolean tie = false;

	public static void main(String[] args) throws IOException {
		String p1, p2;
		System.out.print("Enter name of player 01:  ");
		Scanner s = new Scanner(System.in);
		p1 = s.nextLine();
		System.out.print("Enter name of player 02:  ");
		p2 = s.nextLine();
//		char var1, var2;
		boolean win = false;
		int pos=0;
		Random r = new Random();
		int start = r.nextInt(2);
		if (start == 1) {
			String temp = p1;
			p1 = p2;
			p2 = temp;
		}

		System.out.print(p1 + " Enter the game variable:  ");
		var1 = s.next().charAt(0);
		System.out.print(p2 + " Enter the game variable:  ");
		var2 = s.next().charAt(0);
		System.out.println("Game Starts now");
		System.out.println("-----------------------------------");
		printBoard();
		while (win != true) {
try {
			System.out.print(p1 + " Enter the position b/w 1-9: ");
				pos = s.nextInt();
			
			if (validPos(pos)) {
				insertAtPos(pos, var1);
				printBoard();
				if (checkStatus(var1)) {
					System.out.println(p1 + " has won the game!!");
					resetBoard();
				}else if (tie) {
					resetBoard();
				}
			} 
			else {
			System.out.println("enter the valid position");
			continue;
			}}catch(InputMismatchException ime) {
				System.out.println("enter the valid position"+s.nextLine());
				continue;
			}
			
		
			
		boolean label = true;
		while (label) {
			System.out.print(p2 + " Enter the position b/w 1-9: ");
			try {
				pos = s.nextInt();
			
			if (validPos(pos)) {
				label = false;
				insertAtPos(pos, var2);
				printBoard();
				if (checkStatus(var2)) {
					System.out.println(p1 + " has won the game!!");
					resetBoard();
				} else if(tie)
					resetBoard();

			}
			else
				System.out.println("enter valid position b/w 1-9");
			}catch(InputMismatchException ime) {
				System.out.println("enter the valid position"+s.nextLine());
			}
			
		}

	}
	}

	

	private static void resetBoard() {
		System.out.println("clearing the Board");
		char k = '1';
		for (int i = 0; i < 3; i++)
			for (int j = 0; j < 3; j++)
				boardArray[i][j] = k++;
		System.out.println("do you want to continue? if yes: enter y\n if No: enter n");
		if (new Scanner(System.in).next().equalsIgnoreCase("n")) {
			System.exit(0);
		}
		printBoard();
	}

	private static boolean checkStatus(char var) {
		int i=0;
		char k='1';
		for(i=0;i<3;i++) 
		for(int j=0;j<3;j++)
			if(boardArray[i][j]==k++) 
				return false;
		boolean lucorner = boardArray[0][0] == var ? true : false;
		boolean rucorner = boardArray[0][2] == var ? true : false;
		boolean lbcorner = boardArray[2][0] == var ? true : false;
		boolean rbcorner = boardArray[2][2] == var ? true : false;
		boolean center = boardArray[1][1] == var ? true : false;
		if (center) {
			if ((rucorner && lbcorner) || (lucorner && rbcorner))
				return true;
			else if (boardArray[0][1] == var && boardArray[2][1] == var)
				return true;
			else if (boardArray[1][0] == var && boardArray[1][2] == var)
				return true;
		}
		if (boardArray[0][1] == var)
			if (lucorner && rucorner)
				return true;

		if (boardArray[1][0] == var)
			if (lucorner && lbcorner)
				return true;

		if (boardArray[2][1] == var)
			if (lbcorner && rbcorner)
				return true;

		if (boardArray[1][2] == var)
			if (rucorner && rbcorner)
				return true;
		if(i==3) {
			System.out.println("match tied");
			tie=true;
			return false;
			}
		return false;
		}
	

	private static void insertAtPos(int pos, char variable) {

		switch (pos) {
		case 1:
			boardArray[0][0] = variable;
			break;
		case 2:
			boardArray[0][1] = variable;
			break;
		case 3:
			boardArray[0][2] = variable;
			break;
		case 4:
			boardArray[1][0] = variable;
			break;
		case 5:
			boardArray[1][1] = variable;
			break;
		case 6:
			boardArray[1][2] = variable;
			break;
		case 7:
			boardArray[2][0] = variable;
			break;
		case 8:
			boardArray[2][1] = variable;
			break;
		case 9:
			boardArray[2][2] = variable;
			break;
		default:
			System.out.println("out of range");
		}

	}

	private static boolean validPos(int pos) {
		if (pos < 1 || pos > 9) {
			System.out.println("enntered if");
			return false;
		}

		switch (pos) {
		case 1:
			if (boardArray[0][0] == var1 || boardArray[0][0] == var2)
				return false;
			else
				return true;
		case 2:
			if (boardArray[0][1] == var1 || boardArray[0][1] == var2)
				return false;
			else
				return true;
		case 3:
			if (boardArray[0][2] == var1 || boardArray[0][2] == var2)
				return false;
			else
				return true;

		case 4:
			if (boardArray[1][0] == var1 || boardArray[1][0] == var2)
				return false;
			else
				return true;

		case 5:
			if (boardArray[1][1] == var1 || boardArray[1][1] == var2)
				return false;
			else
				return true;

		case 6:
			if (boardArray[1][2] == var1 || boardArray[1][2] == var2)
				return false;
			else
				return true;

		case 7:
			if (boardArray[2][0] == var1 || boardArray[2][0] == var2)
				return false;
			else
				return true;

		case 8:
			if (boardArray[2][1] == var1 || boardArray[2][1] == var2)
				return false;
			else
				return true;

		case 9:
			if (boardArray[2][2] == var1 || boardArray[2][2] == var2)
				return false;
			else
				return true;

		default:
				return false;
		}

	}

	private static void printBoard() {
		for (int i = 0; i < 3; i++) {
			for (int j = 0; j < 3; j++)
				System.out.print(boardArray[i][j] + "  ");
			System.out.println("");
			System.out.println("");
		}

	}

}
