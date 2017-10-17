@title[Introduction]
# Rapport de <span style="color: #e49436">Stage</span>

#### Fraunhofer Institute
<br>
<br>
<span style="color: #bbb; font-size: 80%">[Institute for Production Systems and Design Technology]</span>


---
@title[Plan]

1. Présentation de Fraunhofer
2. Présentation de l'aile de recherche
3. Projet
4. Gestion de projet
5. Tâches réalisées
6. Conclusion

footnote : "© 2016 One Tap Beyond Inc."

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

- Algorithme de compression <span style="color: #e49436">MP3</span>
- Participation à la création de <span style="color: #e49436">l'AAC</span>
- Records pour panneaux solaires

Note:
MP3: Karlheinz Brandenburg
De nombreuses publications.
---
@title[Employé à Fraunhofer]

### Employés à <span style="color: #e49436">Fraunhofer</span>

- Stagiaire
- Étudiants / Pratikant
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
- <span style="color: #e49436">Création virtuelle produit</span>
- Système production
- Assemblage / revêtement
- Automatisation
- Qualité

Note:
Très bonne ambiance, bière dans tous les bureaux.
Entreprise ouverte tout le temps
Horraires très très flexibles

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

- Problèmes dûs à la <span style="color: #e49436">non connaissance</span> du chef de projet
- Problèmes dûs à la <span style="color: #e49436">non cohérence du projet</span>
- Implication du chef de projet
- Un peu buté parfois

---
@title[Tâches réalisés]

### Sujet de stage

- <span style="color: #e49436">Système de collision</span>
- État de l'art
- Algorithmes à utiliser
- Performances
- Intégration dans la solution

---
@title[Accélération]

### Système de collision

- Problèmes de <span style="color: #e49436">performances</span>
- CPU surchargé
- Utilisation du GPU via <span style="color: #e49436">OpenCL</span>
- Différentes accélération à l'aide <span style="color: #e49436">d'arbres</span>

---
@title[OpenCL impl]

### OpenCL

- Mise en place de classes pour son utilisation
- Gestion <span style="color: #e49436">(presque) automatique</span> de la mémoire
- Mise en place d'exemples pour l'utilisation

---
@title[OpenCL]

###OpenCL

- Utilisation pour augmenter <span style="color: #e49436">performances</span>
- SAT <span style="color: #e49436">(Separate Axis Algorithm)</span>


---
@title[Example]

###Exemple - <span style="color: #e49436">SAT</span>

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
```

Note:
Implémentation du SAT dans un Kernel OpenCL.

---
@title[Example 2]

###Exemple - <span style="color: #e49436">Manage OpenCL</span>

```csharp
public void copyFromBufferGPU(T src, int numElems, int destFirsElem=0, bool waitForCompletion=true)
{
/// <summary>
/// Copy from a buffer to an array.
/// </summary>
    Debug.Assert(numElems+destFirsElem <= this.capacity);
    
    OpenCL.Net.Event clevent;
    OpenCL.Net.ErrorCode status;

    if (numElems + destFirsElem > 0)
    {
        int sizeInBytes = TypeSize<T>.SizeInt * numElems;
        status = Cl.EnqueueWriteBuffer( this._queue, this.buffer, OpenCL.Net.Bool.True, (IntPtr)(TypeSize<T>.SizeInt*destFirsElem), (IntPtr)sizeInBytes, src, 0, null, out clevent);
        CheckErr(status, "copyFromHostPointer");
        if (waitForCompletion)
        {
            status = Cl.Finish(this._queue);
            CheckErr(status, "copyFromHostPointer ClFinished");
        }
    }
}
```

Note:
manage OpenCL

---
@title[Raycast impl]

### Dynamic occlusion

- Mise en place <span style="color: #e49436">raycast</span>
- Accélération <span style="color: #e49436">arbre</span>
- Accélération <span style="color: #e49436">OpenCL</span>
- Remise travail à un autre stagiaire

---
@title[Autre]

### <span style="color: #e49436">Autre</span>

- Reécriture de parties du code
- Amélioration et optimisations
- Correction de bugs
- Tests

---
@title[Formations]

### Formations

- Formation de l'équipe et des stagiaires à <span style="color: #e49436">Git</span>
- Formation conjointe au <span style="color: #e49436">scrum</span> du chef de projet
- Formation d'autres membres de l'équipe sur des points informatiques
<span style="color:gray; font-size:0.6em;">Exemple: Pointeurs, accélération par les arbres, POO et modularisation</span>

---
@title[Conclusion]

### Conclusion

- Très interessante au sein d'un organisme de recherche
- Ambiance et entreprise absorbante, on y passe des heures
- Stagiaire pas tout le temps "sous-catégorisé"
- Sous-payé pour le travail effectué
- Difficultés avec la langue
