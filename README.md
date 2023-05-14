# Module2
Sub Module2()
    Dim Ticker As String
    Dim Ticker_Total As Double
    Dim Yearly_Change As Double
    Dim Percent_change As Double
    Dim Total_Stock As Double
    'Dim Volume As Double
    Dim Ticker_Name As String
    Dim i As Long
    Dim days As Integer
    Dim lastrow As Long
    Dim j As Integer
    Dim start As Long
    
    
    Range("I1").Value = "Ticker"
    Range("J1").Value = "Yearly_Change"
    Range("K1").Value = "Percent_Change"
    Range("L1").Value = "Total_Stock_Volume"
    Range("P1").Value = "Ticker"
    Range("Q1").Value = "Value"
    Range("O2").Value = "Greatest % Increase"
    Range("O3").Value = "Greatest % Decrease"
    Range("O4").Value = "Greatest Total Volume"
    
    'inital values
    j = 0
    Total_Stock = 0
    Yearly_Change = 0
    start = 2

    lastrow = Cells(Rows.Count, 1).End(xlUp).Row
    
    'Dim Summary_Table_Row As long
    'Summary_Table_Row = 2
    
    For i = 2 To lastrow
    
        If Cells(i + 1, 1).Value <> Cells(i, 1).Value Then
        
        
            Total_Stock = Total_Stock + Cells(i, 7).Value
            
            If Total_Stock = 0 Then
                Range("I" & 2 + j).Value = Cells(i, 1).Value
                Range("J" & 2 + j).Value = 0
                Range("K" & 2 + j).Value = "%" & 0
                Range("L" & 2 + j).Value = 0
            Else
                If Cells(start, 3) = 0 Then
                    For findvalue = start To i
                        If Cells(findvalue, 3).Value <> 0 Then
                            start = findvalue
                            Exit For
                        End If
                    Next findvalue
                End If
                Yearly_Change = Cells(i, 6).Value - Cells(i, 3).Value
                
                Yearly_Change_Percent = Yearly_Change / Cells(start, 3)
            
                start = i + 1
        
                Range("J" & 2 + j).Value = Yearly_Change
                Range("J" & 2 + j).NumberFormat = "0.00"
                Range("K" & 2 + j).Value = Yearly_Change_Percent
                Range("K" & 2 + j).NumberFormat = "0.00"
                Range("L" & 2 + j).Value = Total_Stock
                Range("I" & 2 + j).Value = Cells(i, 1).Value
                
                
                Select Case Yearly_Change
                    Case Is > 0
                        Range("J" & 2 + j).Interior.ColorIndex = 4
                    Case Is < 0
                        Range("J" & 2 + j).Interior.ColorIndex = 3
                    Case Else
                        Range("J" & 2 + j).Interior.ColorIndex = 0
                End Select
                
                End If
                Total_Stock = 0
                Yearly_Change = 1
                j = j + 1
                days = 0
                
            Else
                Total_Stock = Total_Stock + Cells(i, 7).Value
            End If
            
        
        Next i
        
    
        Range("Q2") = "%" & WorksheetFunction.Max(Range("K2:K" & lastrow)) * 100
        Range("Q3") = "%" & WorksheetFunction.Min(Range("K2:K" & lastrow)) * 100
        Range("Q4") = WorksheetFunction.Max(Range("L2:L" & lastrow))
        
        increase_number = WorksheetFunction.Match(WorksheetFunction.Max(Range("K2:K" & lastrow)), Range("K2:K" & lastrow), 0)
        decrease_number = WorksheetFunction.Match(WorksheetFunction.Min(Range("K2:K" & lastrow)), Range("K2:K" & lastrow), 0)
        volume_number = WorksheetFunction.Match(WorksheetFunction.Max(Range("L2:L" & lastrow)), Range("L2:L" & lastrow), 0)
        
        Range("P2") = Cells(increase_number + 1, 9)
        Range("P3") = Cells(decrease_number + 1, 9)
        Range("P4") = Cells(volume_number + 1, 9)
    
    
    
End Sub
