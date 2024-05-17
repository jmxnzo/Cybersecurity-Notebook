##### Endlicher Körper
![[Pasted image 20240512210141.png]]


![[Pasted image 20240512210310.png]]
- Ring ist Körper ohne inverses Element, Halbgruppe der Multiplikation 
- Eine _Halbgruppe_ ist ein geordnetes Paar ( H , ∗ ) ![{\displaystyle (H,*)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/1ca9efa8f60b1acd949386d15ff163c637042933) bestehend aus einer Menge H ![{\displaystyle H}](https://wikimedia.org/api/rest_v1/media/math/render/svg/75a9edddcca2f782014371f75dca39d7e13a9c1b) und einer inneren zweistelligen Verknüpfung
∗ : H × H → H , ( a , b ) ↦ a ∗ b , ![{\displaystyle *\colon \,H\times H\to H,\,(a,b)\mapsto a*b,}](https://wikimedia.org/api/rest_v1/media/math/render/svg/26e21f01a31a2d9bb35c5807773d8bf5cb9bc1a3)

die assoziativ ist, d. h. für alle a , b , c ∈ H ![{\displaystyle a,b,c\in H}](https://wikimedia.org/api/rest_v1/media/math/render/svg/50c0d46ddf30f01aab627a682f48b97fca115fc5) gilt

a ∗ ( b ∗ c ) = ( a ∗ b ) ∗ c ![{\displaystyle a*(b*c)=(a*b)*c}](https://wikimedia.org/api/rest_v1/media/math/render/svg/cb031018f88b92239cb9d9a06e2ad32ce39b258c) .
##### Die Existenz endlicher Körper
![[Pasted image 20240512211233.png]]

##### Primzahlkörper
![[Pasted image 20240512211546.png]]


##### Erweiterungskörper GF(2^m)
- innerhalb des AES kommt der endliche Körper GF(2⁸) mit  256 Elementen zum Einsatz, da so jedes Element mit einem Byte dargestellt werden kann
- ist die Ordnung eines Körpers nicht prim (m>1), können Körperaddition und -multiplikation nicht durch modulo p^m realisiert werden -> Erweiterungskörper
- Elemente können als Polynome dargestellt werden und die dazugehörige Polynomarithmetik kann für die Rechenoperationen genutzt werden
![[Pasted image 20240512212439.png]]Jedes Polynom kann einfach in digitaler Form als 8-Bit-Vektor gespeichert werden, der von den acht Polynomkoeffizienten gebildet wird. Insbesondere muss man nicht die Terme x 7, x 6 etc. speichern, da durch die Bitposition klar ist, zu welcher Potenz x i jeder Koeffizient gehört.


##### Addition und Subtraktion in GF(2^m)
![[Pasted image 20240512212652.png]]
-> nichts anderes als XOR-Verknüpfung 
![[Pasted image 20240512212914.png]]
Wir erhielten dasselbe Resultat, wenn wir die Differenz A.x/ 
 B.x/ der beiden Polynome aus obigem Beispiel berechnen würden.



##### Multiplikation in GF(2^m)
- Hauptoperation innerhalb der MixColumn-Transformation des AES
![[Pasted image 20240512214217.png]]
![[Pasted image 20240512214032.png]]

Die bestimmten Polynome, durch die dividiert wird, sind irreduzible Polynome. Wir erinnern uns an Abschn. 2.3.1 und an die Tatsache, dass irreduzible Polynome vergleichbar mit Primzahlen sind, d. h. ihre einzigen Faktoren sind die Zahl 1 und das Polynom selbst.


##### Multiplikativen Inversen der AES-S-Box
- P(x)=x⁸+x⁴+x³+x+1
![[Pasted image 20240512215224.png]]