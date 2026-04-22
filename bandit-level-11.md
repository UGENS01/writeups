"Level 11: The data.txt file contained a ROT13 (Rotate by 13)-encoded password. ROT13 substitutes each letter with the one 13 positions after it in the alphabet. I decoded it using the tr (translate) command, passing the encoded alphabet as the source and the decoded alphabet as the destination:
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
