# iterviewbit--math--next-smallest-palindrome

-----> Question:

Given a numeric string A representing a large number you need to find the next smallest palindrome greater than this number.



Problem Constraints
1 <= |A| <= 100

A doesn't start with zeroes and always contain digits from 0-9.



Input Format
First and only argument is an string A.



Output Format
Return a numeric string denoting the next smallest palindrome greater than A.



Example Input
Input 1:

 A = "23545"
Input 2:

 A = "999"


Example Output
Output 1:

 "23632"
Output 2:

 "1001"
 
 
 
 ------>code:
 string Solution::solve(string s) {
    
    	int n=s.length(),a=0;
	for(int i=0;i<n;i++){
		if(s[i]=='9'){
			a++;
		}
	}
	
	if(a==n){
		string t(a-1,'0');
		return "1"+t+"1";
	}
	
	if(n%2!=0){
		int i=n/2-1,j=n/2+1,mid=n/2;
		
		while(s[i]==s[j]&&i>=0){
			i--;
			j++;
		}

        if(i==-1){
            i=n/2-1;
            j=n/2+1;
            int carry =1;
            while(i>=0 && carry==1){
                if(s[i]=='9'){
                    s[i]='0';
                    s[j]=s[i];
                    carry=1;
                }else{
                    s[i]=s[i]+carry;
                    s[j]=s[i];
                    carry=0;
                }
                i--;
                j++;
            }

        }else if(s[i]>s[j]){
			while(i>=0){
				s[j]=s[i];
				i--;
				j++;
				
			}
		}else if(s[i]<s[j]){
			int b=s[mid]-'0'+1;
			s[mid]=b%10+'0';
			int carry=b/10;
			s[i]=s[i]+carry;
			while(i>=0){
				s[j]=s[i];
				j++;
				i--;
			}
		}
	}else{
		int i=n/2-1,j=n/2;
		
		while(s[i]==s[j]&&i>=0){
			i--;
			j++;
		}

        if(i==-1){
            i=n/2-1;
            j=n/2;
            int carry =1;
            while(i>=0 && carry==1){
                if(s[i]=='9'){
                    s[i]='0';
                    s[j]=s[i];
                    carry=1;
                }else{
                    s[i]=s[i]+carry;
                    s[j]=s[i];
                    carry=0;
                }
                i--;
                j++;
            }

        }else if(s[i]>s[j]){
			while(i>=0){
				s[j]=s[i];
				j++;
				i--;
			}
		}else if(s[i]<s[j]){
			s[i]=s[i]+1;
			while(i>=0){
				s[j]=s[i];
				j++;
				i--;
			}
		}
	}
	
	
	return s;
}
