Function SpellNumber(ByVal MyNumber)
Dim x_string As String
Dim whole_num As Integer
Dim x_string_pnt
Dim x_string_Num
Dim x_pnt As String
Dim x_numb As String
Dim x_P() As Variant
Dim x_DP
Dim x_cnt As Integer
Dim x_output, x_T As String
Dim x_my_len As Integer
On Error Resume Next
x_P = Array("", "Thousand ", "Million ", "Billion ", "Trillion ", " ", " ", " ", " ")
x_numb = Trim(Str(MyNumber))
x_DP = InStr(x_numb, ".")
x_pnt = ""
x_string_Num = ""
If x_DP > 0 Then
x_pnt = " point "
x_string = Mid(x_numb, x_DP + 1)
x_string_pnt = Left(x_string, Len(x_numb) - x_DP)
For whole_num = 1 To Len(x_string_pnt)
x_string = Mid(x_string_pnt, whole_num, 1)
x_pnt = x_pnt & get_digit(x_string) & " "
Next whole_num
x_numb = Trim(Left(x_numb, x_DP - 1))
End If
x_cnt = 0
x_output = ""
x_T = ""
x_my_len = 0
x_my_len = Int(Len(Str(x_numb)) / 3)
If (Len(Str(x_numb)) Mod 3) = 0 Then x_my_len = x_my_len - 1
Do While x_numb <> ""
If x_my_len = x_cnt Then
x_T = get_hundred_digit(Right(x_numb, 3), False)
Else
If x_cnt = 0 Then
x_T = get_hundred_digit(Right(x_numb, 3), True)
Else
x_T = get_hundred_digit(Right(x_numb, 3), False)
End If
End If
If x_T <> "" Then
x_output = x_T & x_P(x_cnt) & x_output
End If
If Len(x_numb) > 3 Then
x_numb = Left(x_numb, Len(x_numb) - 3)
Else
x_numb = ""
End If
x_cnt = x_cnt + 1
Loop
x_output = x_output & x_pnt
SpellNumber = x_output
End Function
Function get_hundred_digit(xHDgt, y_b As Boolean)
Dim x_R_str As String
Dim x_string_Num As String
Dim x_string As String
Dim y_I As Integer
Dim y_bb As Boolean
x_string_Num = xHDgt
x_R_str = ""
On Error Resume Next
y_bb = True
If Val(x_string_Num) = 0 Then Exit Function
x_string_Num = Right("000" & x_string_Num, 3)
x_string = Mid(x_string_Num, 1, 1)
If x_string <> "0" Then
x_R_str = get_digit(Mid(x_string_Num, 1, 1)) & "Hundred "
Else
If y_b Then
x_R_str = "and "
y_bb = False
Else
x_R_str = " "
y_bb = False
End If
End If
If Mid(x_string_Num, 2, 2) <> "00" Then
x_R_str = x_R_str & get_ten_digit(Mid(x_string_Num, 2, 2), y_bb)
End If
get_hundred_digit = x_R_str
End Function
Function get_ten_digit(x_TDgt, y_b As Boolean)
Dim x_string As String
Dim y_I As Integer
Dim x_array_1() As Variant
Dim x_array_2() As Variant
Dim x_T As Boolean
x_array_1 = Array("Ten ", "Eleven ", "Twelve ", "Thirteen ", "Fourteen ", "Fifteen ", "Sixteen ", "Seventeen ", "Eighteen ", "Nineteen ")
x_array_2 = Array("", "", "Twenty ", "Thirty ", "Forty ", "Fifty ", "Sixty ", "Seventy ", "Eighty ", "Ninety ")
x_string = ""
x_T = True
On Error Resume Next
If Val(Left(x_TDgt, 1)) = 1 Then
y_I = Val(Right(x_TDgt, 1))
If y_b Then x_string = "and "
x_string = x_string & x_array_1(y_I)
Else
y_I = Val(Left(x_TDgt, 1))
If Val(Left(x_TDgt, 1)) > 1 Then
If y_b Then x_string = "and "
x_string = x_string & x_array_2(Val(Left(x_TDgt, 1)))
x_T = False
End If
If x_string = "" Then
If y_b Then
x_string = "and "
End If
End If
If Right(x_TDgt, 1) <> "0" Then
x_string = x_string & get_digit(Right(x_TDgt, 1))
End If
End If
get_ten_digit = x_string
End Function
Function get_digit(xDgt)
Dim x_string As String
Dim x_array_1() As Variant
x_array_1 = Array("Zero ", "One ", "Two ", "Three ", "Four ", "Five ", "Six ", "Seven ", "Eight ", "Nine ")
x_string = ""
On Error Resume Next
x_string = x_array_1(Val(xDgt))
get_digit = x_string
End Function
