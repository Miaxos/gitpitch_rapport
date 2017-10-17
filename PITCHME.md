@title[Introduction]
# Rapport de <span style="color: #e49436">Stage</span>

#### Fraunhofer Institute
<br>
<br>
<span style="color: #bbb; font-size: 80%">[ GitHub, GitLab, Bitbucket, GitBucket, Gitea, Gogs ]</span>


---
@title[Plan]

1. Présentation de Fraunhofer
2. Présentation de l'aile de recherche
3. Projet
4. Gestion de projet
5. Tâches réalisées
6. Conclusion

---
@title[Fraunhofer]

#### <span style="color: #e49436">69</span> Instituts en Allemagne
#### Environ <span style="color: #e49436">24084 employés (décembre 2015)</span>

Note:
Il existe également des instituts à l'étranger.
- Chaque institut possède des domaines de recherches
---
@title[Célèbre]

#### Quelques faits célèbres de Fraunhofer

- Algorithme de compression MP3
- Participation à la création de l'AAC
- Records pour panneaux solaires

Note:
MP3: Karlheinz Brandenburg
De nombreuses publications.
---
@title[Employé à Fraunhofer]

### Employés à Fraunhofer

- Stagiaire
- Étudiants
- Diplômé, administration, maintenance;

Note:
Stagiaire : 2% des employés, 3 mois / 6 ou 1 an.
Travail sous un ou plusieurs scientifiques, projet public ou privé.
Étudiants: 28%
Diplomé: diriger, trouver des partenaires et financement etc.

---
@title[Organisation à Fraunhofer]

### Dirigé par un professeur

- <span style="color: #e49436">Eckart Uhlmann</span> dirige IPK Fraunhofer

### Branches

- Gestion entreprise
- Création virtuelle produit
- Sustème production
- Assemblage / revêtement
- Automatisation
- Qualité

Note:
Très bonne ambiance, bière dans tous les bureaux.
Entreprise ouverte tout le temps
Horraires très très flexibles

---
@title[Un modèle qui marche]

### Un modèle qui marche
- Le modèle Fraunhofer
- Contrats d'entreprises
- Contrats public
- Budget: <span style="color: #e49436">2,1 milliards</span> d'euros <span style="color: #e49436">(2015)</span>

Note:
Financement 30% par état et le reste par contrats

---
@title[Aile de recherche]

### Création virtuelle produit

- Industrie 4.0
- Réalitée virtuelle dans l'industrie
- Réalitée augmentée dans l'industrie
- <span style="color: #e49436">60 personnes</span>

Note:
Focus sur ces sujets, mais après d'autres projets étaient disponibles.
- Industrie 4.0
- Multitude de bureaux
- Beaucoup de physiciens et ingénieurs

---
@title[Projet]

### Projet

Un <span style="color: #e49436">prototype</span> fait sous Unity qui devait permettre aux utilisateurs de <span style="color: #e49436">se connecter ensemble</span> et d'effectuer différentes <span style="color: #e49436">interactions</span> sur le modèle, <span style="color: #e49436">sauvegarder ces informations</span>, de façon simple et ergonomique en utilisant la réalité virtuelle.

---
@title[Gestion de projet]

### Gestion de projet

- Problèmes dûs à la non connaissance du chef de projet
- Problèmes dûs à la non cohérence du projet
- Problèmes dûs à l'absence du chef de projet

---
@title[Tâches réalisés]

### Sujet de stage

- <span style="color: #e49436">Système de collision</span>
- État de l'art
- Algorithmes à utiliser
- Performances
- Intégration dans la solution

---
@title[Step 1. Create 'PITCHME.md']

```c
__kernel void satTriangleAABBKernel(
	int numTriangles,
	int trianglesPerThread,
	__global float4* meshVertices, 
	__global int* meshTriangles,
	__global float4* aabbVertices,
	__global int* result
	)
{
	int i = get_global_id(0);

	for (int j = i*trianglesPerThread; j < (i+1)*trianglesPerThread && j < numTriangles; j++)
	{
		//getting triangle vertices
		float4 triangleVertice0 = meshVertices[meshTriangles[3*j]];
		float4 triangleVertice1 = meshVertices[meshTriangles[3*j + 1]];
		float4 triangleVertice2 = meshVertices[meshTriangles[3*j + 2]];
		
		if (triangleIntersectsAabb(triangleVertice0, triangleVertice1, triangleVertice2, aabbVertices))
		{
			atomic_add(&result[0], 1);
			break;			
		}
		
		
	}
}
````
---
@title[Step 1. Create 'PITCHME.md']

### <span style="color: #e49436">STEP 1. Create 'PITCHME.md'</span>
<br>

#### Create GitPitch slideshow content using GitHub Flavored Markdown in your favorite editor.

<br>
<span style="color:gray; font-size:0.6em;">[ AS EASY AS README.md ]</span>

---
@title[Step 2. Git-Commit]

### <span style="color: #e49436">STEP 2. GIT-COMMIT</span>
<br>

```shell
$ git add PITCHME.md
$ git commit -m "New slideshow content."
$ git push

Done!

```

@[1](Add your PITCHME.md slideshow content file.)
@[2](Commit PITCHME.md to your local repo.)
@[3](Push PITCHME.md to your public repo and you're done!)
@[5](Supports GitHub, GitLab, Bitbucket, GitBucket, Gitea, and Gogs.)

---
@title[Step 3. Done!]

### <span style="color: #e49436">STEP 3. GET THE WORD OUT!</span>

<br>

<span style="font-size: 1.3em;"><span style="color:white">htt</span><span style="color:white">ps://git</span><span style="color: #e49436">pitch</span><span style="color: white">.com/<span style="color: #e49436">user</span>/<span style="color: #e49436">repo</span>/<span style="color: #e49436">branch</span></span>

<br>

#### Instantly use your GitPitch slideshow URL to promote, pitch or present absolutely anything.

---
@title[Slide Rich]

### <span style="color: #e49436">Slide Rich</span>

#### Code Presenting for Blocks, Files, and GISTs
#### Image, Video, Chart, and Math Slides
#### Multiple Themes With Easy Customization
<br>
#### <span style="color: #e49436">Plus collaboration is built-in...</span>
#### Your Slideshow Is Part Of Your Project
#### Under Git Version Control Within Your Git Repo

---

@title[Feature Rich]

### <span style="color: #e49436">Feature Rich</span>

#### Present Online or Offline
#### With Speaker Notes Support
#### Print Presentation as PDF
#### Auto-Generated Table-of-Contents
#### Share Presentation on Twitter or LinkedIn

---

### Go for it.
### Just add <span style="color: #e49436; text-transform: none">PITCHME.md</span> ;)
<br>
<a style="font-size:0.6em;" href="https://github.com/gitpitch/gitpitch/wiki">[ Click To Learn More On Wiki ]</a>