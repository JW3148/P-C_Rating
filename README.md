# P&C_Rating, Data Analytics

Note on basic rate making for P&C insurance

Based on CAS textbook [Basic Ratemaking]


Internal data
-risk data(exposures, premium, claim, losses..)
-accounting data(underwriting expense, ULAE...)

Important! understant the granularity first! What a record means?

Both policy database and claim database usually be transactional

Policy Database
-Granularity: individule policy or further subdivision of the policy
-fields: explantory info on the records
-homeowner insurance: a record may be home for an annual policy period(one home, one year)
-workers compensation: classification level, each policynumber divided into different class
-personal auto: typically at coverage level, may be records for each auto, or operator for each auto(one auto can be insured for two drivers)
policy, insured items, coverage, operater. for example, an auto policy insuring two drivers on two cars for six coverage could involve 24 records

Cancellation
-add a new record in policy info table 
-in field, will have a transaction effect date
-written exposure will be -0.25 if you are cancelling at 75% of the policy period
-written premium will be -150, assuming that you need to return 150 to customer

Change in deductible
- will bring in two extra record
- new record1: cancelling the remaining period
- new record2: new record for the remaining period with updated deductible

Claim Database
- may also be defined at different levels, e.g. claims involving mutiple coverages or causes of loss may be recorded as seperated records
- one claim may have subdivisions
- have loss information

Report Claim
-open a new reocrd the reported claim
-set a initial case reserve
-claim status: open

Payment of Claim
-add new record for that claim, with the loss payment and new case reserve
-claim status: open

Pay off a Claim
-add new record for that claim, with the loss payment, and set case reserve to 0
-claim status: close

Loss of a policy(throught out the policy period)=Total loss payment
Loss during a certain period=Total loss payment during the period + changed in case reserve in the period


Salvage/subrogation
- if a company replace a property, the company assumes owership of the old damanged propery
- the damanged property may then be reconditioned and sold to offset part of the payment made
- these recoveries are called salvage

Accouting data
-UW expenses
-LAE(ALAE+ULAE)

Data Aggregation(three general objectives)
- Accurately match losses and premium for the policy
- Use the mose recent data available
- Minimize the cost of data retrieval

Calendar year aggregation(can be calandar quarter, month..)
- premium: all premium and exposure earned during that 12 month period
- loss: reported loss during that 12 month peroid(paid loss+ change in case reserve)
- pros: once that period ends, data will be available, i.e. when you reach the end of period, all earned premium and reported loss are certain
- cons: loss and premium may come from diffrent policies, the loss paid in year may comes from a policy years ago. the premium will be from a 
a recent writted policy(this year or prevous year)

Accident year aggregation(also called calandar-accident year)
- only considers losses that associated with an accident that happend in that 12 month period
- interested in losses happen during this period
- first find all accidents/events happened in the 12 month period
- losses: the losses for the above accidents, for example, in 2009, 2080 accident happens, what are their losses?
losses=paid loss for those accident + case reserve for those accident + furture loss development for those accident(need to estimate)
- premium: follows same rule as calendar year
- pros: accidents happened this period are covered by policies written in this period or previous one
- cons: need to estimate loss development; accidents happened this period shoud come from policies written in this period or previos one
at the end of the period, you still don't have all the accident happend in this period, they may just now be reported yet, usually there will
be delay in report a accident


Policy year aggregation(also call underwritten year)
- only considers the group of policy issued during this 12 month period
- let's call them group A policies
- premium: premium for group A policies(need to estimate what's the ultimate amount
- losses: losses on group A polices(ultimate loss=paid loss at this point+  case reserve at this point + ibnr at this point+ new claims i the future)
- pros: best match
- cons: takes time to develop/envolve

Report year aggregation
- interested in claims reported during the period
- clam reported this period can be covered by a policy way back than - mismatch




Inscured loss(reported, not reported)
-reported(paid losses + case reserve) --> may change over time when more info 
