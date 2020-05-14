# Sudoku-Solver-In-Java

import java.math.*;
import java.util.*;


public class Node{

    public static void main (String args[]) 
    { 
    	ArrayList<ArrayList<Character>> a=new ArrayList<>();
    	ArrayList<Character> temp=new ArrayList<>();
    	temp.add('5');
    	temp.add('3');
    	temp.add('.');
    	temp.add('.');
    	temp.add('7');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('6');
    	temp.add('.');
    	temp.add('.');
    	temp.add('1');
    	temp.add('9');
    	temp.add('5');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('.');
    	temp.add('9');
    	temp.add('8');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('6');
    	temp.add('.');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('8');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('6');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('3');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('4');
    	temp.add('.');
    	temp.add('.');
    	temp.add('8');
    	temp.add('.');
    	temp.add('3');
    	temp.add('.');
    	temp.add('.');
    	temp.add('1');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('7');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('2');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('6');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('.');
    	temp.add('6');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('2');
    	temp.add('8');
    	temp.add('.');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('4');
    	temp.add('1');
    	temp.add('9');
    	temp.add('.');
    	temp.add('.');
    	temp.add('5');
    	a.add(temp);
    	
    	temp=new ArrayList<>();
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('.');
    	temp.add('8');
    	temp.add('.');
    	temp.add('.');
    	temp.add('7');
    	temp.add('9');
    	a.add(temp);
    	
    	solveSudoku(a);
    	for(int i=0;i<9;i++)
    	{
    		for(int j=0;j<9;j++)
    		{
    			System.out.print(bd[i][j]+" ");
    		}
    		System.out.println();
    	}
    }
    
    
    static int n = 9;
    static int bd[][] = new int[n][n];
    
    public static void solveSudoku(ArrayList<ArrayList<Character>> a) {
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(a.get(i).get(j) == '.') {
                    bd[i][j] = 0;
                    continue;
                }
                bd[i][j] = Character.getNumericValue(a.get(i).get(j));
            }
        }
        
        solve(0, 0);
        
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                char c = (char) (bd[i][j] + '0');
                a.get(i).set(j, c);
            }
        }
    }
    
    private static boolean solve(int row, int col) {
        if(row == n) return true;
        if(col == n) return solve(row + 1, 0);
        if(bd[row][col] != 0) return solve(row, col + 1);
        
        for(int i = 1; i < 10; i++) {
            if(isValid(i, row, col)) {
                bd[row][col] = i;
                if(solve(row, col + 1)) return true;
                bd[row][col] = 0;
            }
        }
        return false;
    }
    
    private static  boolean isValid(int val, int row, int col) {
        for(int j = 0; j < n; j++) {
            if(bd[row][j] == val) return false;
        }
        
        for(int i = 0; i < n; i++) {
            if(bd[i][col] == val) return false;
        }
        
        row = (row / 3) * 3;
        col = (col / 3) * 3;
        for(int i = row; i < row + 3; i++) {
            for(int j = col; j < col + 3; j++) {
                if(bd[i][j] == val) return false;
            }
        }
        
        return true;
    }
    
 }
