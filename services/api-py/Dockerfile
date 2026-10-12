# The base image is pinned by digest as well as tag: a tag can be repointed at a different image.
# Dependabot updates both together.
FROM python:3.14-slim@sha256:a2b82f3c48559aa0a8446d9af49826b6e2b2016f4cd2afabfe6013ec53729170
WORKDIR /app
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONPATH=/app/src
# No runtime dependencies, so nothing is installed: the service is the standard library plus this
# source tree. A project that adds dependencies installs them here from the committed uv.lock.
# pip then leaves the image: nothing at runtime calls it, and it vendors packages of its own, with
# vulnerabilities of their own (the image scan found two there and nowhere else).
RUN python -m pip uninstall --yes --root-user-action=ignore pip
COPY src ./src
USER nobody
EXPOSE 8080
CMD ["python", "-m", "api_py.main"]
