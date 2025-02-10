#!/data/data/com.termux/files/usr/bin/bash

# Warna output
RED='\033[0;31m'
GREEN='\033[0;32m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# File log untuk menyimpan hasil tes
LOGFILE="$HOME/speedtest_results.log"

# Cek apakah speedtest-cli sudah terinstal
if ! command -v speedtest-cli &> /dev/null
then
    echo -e "${RED}Speedtest-cli tidak ditemukan! Menginstal sekarang...${NC}"
    pkg install python -y
    pip install speedtest-cli
fi

# Menjalankan Speedtest
echo -e "${BLUE}Menjalankan tes kecepatan internet...${NC}"
RESULT=$(speedtest-cli --simple)

# Menampilkan hasil
echo -e "${GREEN}=== Hasil Speedtest ===${NC}"
echo -e "$RESULT"
echo -e "======================="

# Menyimpan hasil ke log file
echo -e "$(date)\n$RESULT\n=======================\n" >> "$LOGFILE"

# Menampilkan lokasi log file
echo -e "${BLUE}Hasil tes telah disimpan di:${NC} $LOGFILE"
