Select Case When PLANT='A-F' Then 'A-F' 
            When PLANT in('G','A-F') Then 'A-G'
            When  PLANT in ('A-F','G','H') Then 'A-H'
            When  Plant in ('A-F','G','H','I') Then 'A-I' 
            Else NUll End Plant,SUM(LD1_TONS_ACTUAL) LD1_TONS_ACT
            From DEMO.T_LADLE WHERE DATE_TIME>='01-APR-2026' AND DATE_TIME<='13-APR-2026'
            Group by 
            Case When PLANT='A-F' Then 'A-F' 
            When PLANT in ('G','A-F') Then 'A-G'
            When  PLANT in ('A-F','G','H') Then 'A-H'
            When  Plant in ('A-F','G','H','I') Then 'A-I'
            Else NUll End
            Order by Plant
