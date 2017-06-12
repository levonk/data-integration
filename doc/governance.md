# Data Governance

## Intorductions

*A successful Data Governance program can only exist if both technology and business are on board.*

It's also important to note that Data Governance is a spectrum of service with tradeoffs.  On the no data governance level, there is a lot of agility to be gained with the associated risks.  On the full level of governance there will be a significant impact to delivery.   A recommended pattern is to allow data to come in and governance to layered on rather than becoming a blocker in delivery.

## Data Definition
It's critical that Data have unambiguous meanings.  If somebody asks for "Gross Box Office" the term should be sufficient to determine whether it is referring to domestic theatrical opening weekend or inception to date across in theater as well as the home entertainment & streaming space in all territories.  It should also be clear whether it was inflation adjusted or currency converted to the US Dollar and whether it is Net or Gross.  An example might be "Gross Box Office: the US Dollar non-inflation adjusted gross box office receipts for all territories during the entire first theatrical run"  If the reference doesn't satisfy the entire explanation, then there should be a different name that the data is known by.  This applies as strongly to derived data as it does to supplied data.

## Data Freshness
Understanding the Service Level Agreements (SLAs) associated with all the data and the expected freshness of the data will need to be negotiated with the Data Supplier as well as the Integration teams.

## Data Quality
The Governance team must assess the quality of the data sources and assure that the quality is documented within the dictionary.   It would also benefit the team to identify better sources for the data in question.

## Data Usability
Mapping data to master data is a key responsblity of the Data Governance team.  The role of the Data Stewards on the governance team also includes reviewing the "linkability" that the automated systems have suggested or completed.

## Security
It is the role of the data governance team to empower those that would be doing analysis.   This includes supplying alternatives (Homomorphic encryption, lower resolution data, etc...) when there is data that could do ireperable harm should an analyst abuse it.

## Compliance
The governance team needs to identify the risks associated with the data that they are responsible for including any domestic and intenational laws, as well as compny policy that must adhered to.  This includes HIPPA, PII, PCI, etc...  The Governance team will also need to assure that the processes are requested and in place to assure this compliance.

## Communication
Promoting the data sets for use within and around the line of business is a critical responsibility for the Data governance team.  The Data governance team will have the best grasp of the potential uses of the data throughout the organization.
