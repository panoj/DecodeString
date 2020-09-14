# DecodeString
public string Decode(string input) {
            if (input == null || input == string.Empty)
                return string.Empty;

            Stack<char> charStack = new Stack<char>();;

            for (int i = 0; i < input.Length; i++)
                if (input[i] != ']')
                    charStack.Push(input[i]);
                else
                {
                    List<char> temp = new List<char>();
                    int j = 0,
                        k = 0;

                    while (charStack.Count > 0 && charStack.Peek() != '[')
                        temp.Add(charStack.Pop());

                    if (charStack.Count > 0 && charStack.Peek() == '[')
                        charStack.Pop();

                    while (charStack.Count > 0 && (charStack.Peek() >= '0' && charStack.Peek() <= '9'))
                        j += (charStack.Pop() - '0') * (int)Math.Pow(10, k++);

                    for (int l = 0; l < j; l++)
                        for (int m = temp.Count - 1; m > -1; m--)
                            charStack.Push(temp[m]);
                }
            
            return new string(charStack.ToArray().Reverse().ToArray());
    }
}
