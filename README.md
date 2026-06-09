  Begin
        For k in (Select DATE_TIME,FUR_NAME,SAMPLE_ID,AVG(DECODE(S,0,NULL,S))S,AVG(DECODE(C,0,NULL,C))C,AVG(DECODE(MN,0,NULL,MN))MN,
                AVG(DECODE(P,0,NULL,P))P,AVG(DECODE(SI,0,NULL,SI))SI,AVG(DECODE(AL,0,NULL,AL))AL,AVG(DECODE(CU,0,NULL,CU))CU,
                AVG(DECODE(CR,0,NULL,CR))CR,AVG(DECODE(NICKEL,0,NULL,NICKEL))NICKEL,AVG(DECODE(MO,0,NULL,MO))MO,AVG(DECODE(V,0,NULL,V))V,
                AVG(DECODE(NB,0,NULL,NB))NB,AVG(DECODE(TI,0,NULL,TI))TI,AVG(DECODE(B,0,NULL,B))B,AVG(DECODE(W,0,NULL,W))W,
                AVG(DECODE(CO,0,NULL,CO))CO,AVG(DECODE(MG,0,NULL,MG))MG,AVG(DECODE(FE,0,NULL,FE))FE,AVG(DECODE(SN,0,NULL,SN))SN,
                AVG(DECODE(SB,0,NULL,SB))SB,AVG(DECODE(PB,0,NULL,PB))PB,AVG(DECODE(BI,0,NULL,BI))BI,AVG(DECODE(SE,0,NULL,SE))SE,
                AVG(DECODE(CE,0,NULL,CE))CE,AVG(DECODE(LA,0,NULL,LA))LA,AVG(DECODE(TE,0,NULL,TE))TE From TMET.T_TSMD_BF_HOT_METAL_ANAL 
                Where DATE_TIME>=vStdate AND  REGEXP_SUBSTR(k.SAMPLE_ID, '[A-Z][0-9]?$', 1, 1) Group By DATE_TIME,FUR_NAME  Order By DATE_TIME,FUR_NAME,SAMPLE_ID)  
                Loop
                    Update TMET.T_TSMD_BF_HOT_METAL_ANAL_DAILY SET
                    S=k.S,
                    C=k.C,
                    MN=k.MN,
                    P=k.P,
                    SI=k.SI,
                    AL=k.AL,
                    CU=k.CU,
                    CR=k.CR,
                    NICKEL=k.NICKEL,
                    MO=k.MO,
                    V=k.V,
                    NB=k.NB,
                    TI=k.TI,
                    B=k.B,
                    W=k.W,
                    CO=k.CO,
                    MG=k.MG,
                    FE=k.FE,
                    SN=k.SN,
                    SB=k.SB,
                    PB=k.PB,
                    BI=k.BI,
                    SE=k.SE,
                    CE=k.CE,
                    LA=k.LA,
                    TE=k.TE
                Where DATE_TIME>=Trunc(k.DATE_TIME)+6/24 AND DATE_TIME<TRUNC(k.DATE_TIME)+1+6/24 AND FUR_NAME=k.FUR_NAME  ;
        End Loop;    
        Commit;
