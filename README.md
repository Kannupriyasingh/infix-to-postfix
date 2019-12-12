
#include<bits/stdc++.h>
using namespace std;


int prec(char c)
{   if(c == '()')
return 4;
	else if(c == '^'|| c =='$')
	return 3;
	else if(c == '*' || c == '/')
	return 2;
	else if(c == '+' || c == '-')
	return 1;
	else
	return -1;
}


void infixToPostfix(string s)
{
	std::stack<char> st;
	st.push('N');
	int l = s.length();
	string ns;
	for(int i = 0; i < l; i++)
	{
		// If the scanned character is an operand, add it to output string.
		if((s[i] >= 'a' && s[i] <= 'z')||(s[i] >= 'A' && s[i] <= 'Z'))
		ns+=s[i];

		else if(s[i] == '(')

		st.push('(');


		else if(s[i] == ')')
		{
			while(st.top() != 'N' && st.top() != '(')
			{
				char c = st.top();
				st.pop();
			ns += c;
			}
			if(st.top() == '(')
			{
				char c = st.top();
				st.pop();
			}
		}


		else{
			while(st.top() != 'N' && prec(s[i]) <= prec(st.top()))
			{
				char c = st.top();
				st.pop();
				ns += c;
			}
			st.push(s[i]);
		}

	}

	while(st.top() != 'N')
	{
		char c = st.top();
		st.pop();
		ns += c;
	}

	cout << ns << endl;

}

int main()
{
	string exp = "K+L-M*N+(O^P)*W/U/V*T+Q";
	infixToPostfix(exp);
	return 0;
}

