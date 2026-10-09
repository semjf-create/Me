# Voxface backend (squelette)

API d'avatars parlants. Les étapes IA sont simulées : la tâche passe par
voix, animation et rendu, puis renvoie un faux fichier vidéo.

## Lancer en local

    python -m venv .venv && source .venv/bin/activate
    pip install -r requirements.txt
    uvicorn main:app --reload

Documentation interactive : http://127.0.0.1:8000/docs

## Essayer avec curl

    curl -F photo=@visage.jpg -F "text=Bonjour !" -F voice=claire -F style=cartoon -F consent=true \
      http://127.0.0.1:8000/avatars
    curl http://127.0.0.1:8000/avatars/<job_id>
    curl http://127.0.0.1:8000/avatars
    curl -X DELETE http://127.0.0.1:8000/avatars/<job_id>

L'utilisateur est lu dans l'en-tête `X-User-Id` (valeur par défaut : demo).

## À brancher ensuite

- `generate_voice` : API de synthèse vocale.
- `animate_face` : modèle « talking head ».
- `render_video` : assemblage MP4 avec ffmpeg et filigrane « généré par IA ».
- `detect_single_face` : détecteur de visage réel.
- `jobs` : base de données à la place du dictionnaire en mémoire.
- `BackgroundTasks` : file de tâches (Celery, RQ) pour les traitements longs.
- Suppression automatique des fichiers après 30 jours (`expires_at`).
- Authentification réelle à la place de `X-User-Id`.
