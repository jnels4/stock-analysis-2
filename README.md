# stock-analysis-2

## Project Overview

Our client was interested in recommending a "green" stock to their parents.  They were particularly interested in 12 stocks to begin with, with the focus on ticker "DQ", as the "green" stock they were looking to recommend.  We suggested looking at stock performance of a few related stocks during 2017 and 2018.  We analyzed the total trading volume and the percent return over the course of these years individually.  We then used this analysis to provide feedback to our client so that they could recommend a stock to their parents. 


## Results

We analyzed the stock data from 2017 and 2018 and were able to garner some information on the trends of the "DQ" stock in particular, but also of 11 other stocks that our client was interested in.  Once we gave him the first deliverable (analysis of the 12 stocks), our client wanted to expand their view to include an analysis of "X" number of stocks, that would potentially include every ticker in the market, in order to do that, we had to refactor our code to increase effciency.

### Analysis Overview

Firstly, we focused on the 12 stocks provided by our client.  2017 and 2018 provided vastly different results.

**2017**

2017 provided us with an overall postive outlook for these 12 stocks, as all but one showed positive returns.  In fact, the "DQ" stock that our client was interested in showed a 199% return over the course of 2017.  Had we only analyzed the 2017 data, this stock (amongst others) would have been a strong buy, or at least in the coversation for recommendations.  Seeing as how our client wanted the best picture of the data we could feasibly present, we wanted to look at how "DQ" and the 12 other "green" stocks performed in 2018.

<img width="242" alt="2017 Data" src="https://user-images.githubusercontent.com/6634774/164778987-472f5cdc-dcda-4a08-8a75-61174999e4c9.png">

**2018**

2018 provided us with very different stock performance outcomes.  In particular the "DQ" stock did not perform well, despite being traded more, the stock return was down 62.6%.  This stock was no longer a good buy for our client, and would not be a good reccommendation for his parents.  "ENPH" and "RUN" both showed strong trading volumes; as well as, postive returns for 2017 and 2018, so we could be cautiously optimistic with our client to reccommend these stocks to his parents.

<img width="244" alt="2018 Data" src="https://user-images.githubusercontent.com/6634774/164779414-89f0fa87-1f4a-4da7-8428-6d1c96c2b00d.png">

### Going Further

We provided our client with our first deliverable, an analysis of the 12 stocks requested for the years 2017 and 2018, and they were optimistic, but felt that they needed more information.  We agreed and suggested that we spend some time refactoring our analysis code to improve it's effciency and runtime.  We tested this on the same set of data and found that our code was indeed marginally faster.

Original code ran with 2017 and 2018 data.

<img width="258" alt="Original Code 2017" src="https://user-images.githubusercontent.com/6634774/164780740-7bb5007d-63e0-472a-b353-af217c6f81de.png"><img width="257" alt="Original Code 2018" src="https://user-images.githubusercontent.com/6634774/164780793-ded9bd7b-4102-43c3-ae0c-5ff44139056a.png">

Refactored code ran with 2017 and 2018 data.

<img width="250" alt="Refactor 2017" src="https://user-images.githubusercontent.com/6634774/164780932-a53b41e3-0815-42d8-97ce-66a2514221df.png"><img width="253" alt="ReFactor 2018" src="https://user-images.githubusercontent.com/6634774/164780934-19fe3b7d-bfc9-439e-8481-ddc83488f84c.png">

*ReFactoring*

To reFactor our code, we needed to think about scalability.  Our code worked great with a few thousand records, but what if there were 100,000 or even 1,000,000 or X records?

Our original code both calculated and wrote directly to our spreadsheet within one set of nested loops.  While this may *seem* efficient, it actually isn't.

    
      'For i = 0 To 11
        Worksheets(yearValue).Activate
        ticker = tickers(i)

        ' iterate through the year spreadsheet
        For j = rowStart To rowEnd
        
            If (Cells(j, 1).Value = ticker) Then
                 totalVolume = totalVolume + Cells(j, 8).Value
            End If
        
        'set starting price based on ticker value
        
            If (Cells(j, 1).Value = ticker And Cells(j - 1, 1).Value <> ticker) Then
                startingPrice = Cells(j, 6).Value
            End If
        
        'set ending price based on ticker value
            If Cells(j, 1).Value = ticker And Cells(j + 1, 1).Value <> ticker Then
                 endingPrice = Cells(j, 6).Value
           End If
        Next j
        
        'Calculations, write info in cells
        Worksheets("All Stocks Analysis").Activate
        Cells(i + 5, 1).Value = ticker
        Cells(i + 5, 2).Value = totalVolume
        returnVal = (endingPrice / startingPrice) - 1
        Cells(i + 5, 3).Value = returnVal
        
        'Evaluate Return val to assign color
        If (returnVal < 0) Then
            Cells(i + 5, 3).Interior.Color = vbRed
        ElseIf (returnVal > 0) Then
            Cells(i + 5, 3).Interior.Color = vbGreen
        Else
            Cells(i + 5, 3).Interior.Color = xlNone
        End If
        
        'Reset all variables for next ticker
        totalVolume = 0
        returnVal = 0
        startingPrice = 0
        endingPrice = 0
    Next i


To scale our code for larger datasets and reduce the runtime, we created an array to hold all of the information, this way we were not doing calculations in time for each index, rather per index using a nested for loop.  Due to the fact that we used mutliple arrays to hold all of our information, we could easily iterate through the array using a "tickerIndex", that would pull the correct information based on the assigned index for each tickers index.  Additionally, rather than using this format to write directly to our spreadsheet, we stored all of then necessary information into separate arrays, and used a separate loop to write this that information to our spreadsheet.  Using this new method, we decreased our 2017 runtime by 8.4% and our 2018 runtime by 8.5%.  

  
    
    'Create three output arrays
    Dim tickerVolumes(12) As Long
    Dim tickerStartingPrices(12) As Single
    Dim tickerEndingPrices(12) As Single
    
    ' Create a for loop to initialize the tickerVolumes to zero.
    For tickerIndex = 0 To 11
        Worksheets(yearValue).Activate
        tickerVolumes(tickerIndex) = 0
        ticker = tickers(tickerIndex)

    
        
    ' Loop over all the rows in the spreadsheet.
        For i = 2 To RowCount
            
        'Increase volume for current ticker
            If (Cells(i, 1).Value = ticker) Then
                tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value
            End If
        'Check if the current row is the first row with the selected tickerIndex.
        
            
             If (Cells(i, 1).Value = ticker And Cells(i - 1, 1).Value <> ticker) Then
                tickerStartingPrices(tickerIndex) = Cells(i, 6).Value
            End If
            
        
        'check if the current row is the last row with the selected ticker
         'If the next row’s ticker doesn’t match, increase the tickerIndex.
            If Cells(i, 1).Value = ticker And Cells(i + 1, 1).Value <> ticker Then
                 tickerEndingPrices(tickerIndex) = Cells(i, 6).Value
           End If
        Next i
        
        

            Increase the tickerIndex.
    Next tickerIndex
        
    
    Loop through your arrays to output the Ticker, Total Daily Volume, and Return.
    For i = 0 To 11
        
        Worksheets("All Stocks Analysis").Activate
        Cells(i + 4, 1).Value = tickers(i)
        Cells(i + 4, 2).Value = tickerVolumes(i)
        Cells(i + 4, 3).Value = (tickerEndingPrices(i) / tickerStartingPrices(i)) - 1
        
    Next i


##Summary

1. The advantages of reFactoring code allows us to consider the scalablity of our analysis.  While we may start with a small data set, we may want to do the same or similar analysis on a larger or infinitely larger dataset, by refacoring our code we can improve our effciency and our ability to handle large/demanding data sets.  This also allows us to create code that is flexible and adaptable to the dataset we are using regardless of the size.

2. By refactoring we were able to clearly improve our efficiency on this small dataset by 8.4% and 8.5% (2017/2018).  Since our dataset was only a few thousand rows (3013 for both), we did not have a larger dataset to test it on, we can only assume that our refactoring efficiency increase will hold on a larger dataset.  Extrapolating our effciency improvements, if we had a dataset that would normally take 30 minutes to run using our old methodology, our new reFactored code would improve that time by ~2min 30 sec, and it would take 27min 30 seconds to run that same data.

