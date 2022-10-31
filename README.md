- 👋 Hi, I’m @LYSAILY
- 👀 I’m interested in forest ecology and community
- 🌱 I’m currently learning R 
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
LYSAILY/LYSAILY is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->重要值计算
for (i in 2:6) {
sh <- read.xlsx("IVTable.xlsx",i)
num.spe <- table(unlist(sh$spe))
RA <- num.spe/sum(num.spe)
sharea.c <- (sh$p/pi/2)^2*pi 
spe.area.c <- tapply(sharea.c,sh$spe, sum) 
area.c.all <- sum(spe.area.c)
r.dominance <- spe.area.c/sum(area.c.all)
freq_table <- table(sh$plot,sh$spe) 
freq_TF <- summary(freq_table >0)[3,]
freq <- as.numeric(str_extract(freq_TF, '[0-9]+'))
r.freq <- freq/sum(freq)
sh.IV <- data.frame(num.spe, RA, r.dominance, r.freq) 
sh.IV <- sh.IV$Freq + sh.IV$r.dominance + sh.IV$r.freq
sh.IV <- as.data.frame(sh.IV)
sh.IV <- data.frame(num.spe, sh.IV)
write.csv(sh.IV, file = paste0("IV", i, ".csv", sep = ""))
}
