decimal FurFaceValue = 0;

if (maturityPerc == 0)
{
    FurFaceValue = 0.5m;
}
else if (totalRunningHr > 1450 ||
         FurCircuit == "G" ||
         FurCircuit == "H" ||
         FurCircuit == "I")
{
    FurFaceValue = 1;
}
else
{
    FurFaceValue = 0;
}
