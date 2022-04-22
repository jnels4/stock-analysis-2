# stock-analysis-2

## Project Overview

Our client was interested in recommending a "green" stock to their parents.  They were particularly interested in 12 stocks to beginwith with the focus on ticker "DQ", as the "green" stock they were looking to recommend.  We suggested looking at stock performance of a few related stocked during 2017 and 2018.  We analyzed the total trading volume and the percent return over the course of these years individually.  We then used this analysis to provide feedback to our client so that they could recommend a stock to their parents. 


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
<img width="258" alt="Original Code 2017" src="https://user-images.githubusercontent.com/6634774/164780740-7bb5007d-63e0-472a-b353-af217c6f81de.png">
<img width="257" alt="Original Code 2018" src="https://user-images.githubusercontent.com/6634774/164780793-ded9bd7b-4102-43c3-ae0c-5ff44139056a.png">

Refactored code ran with 2017 and 2018 data.

<img width="250" alt="Refactor 2017" src="https://user-images.githubusercontent.com/6634774/164780932-a53b41e3-0815-42d8-97ce-66a2514221df.png">
<img width="253" alt="ReFactor 2018" src="https://user-images.githubusercontent.com/6634774/164780934-19fe3b7d-bfc9-439e-8481-ddc83488f84c.png">

